# Architecture Diagram — System Overview

## System Boundary & Data Flow

```mermaid
graph TB
    subgraph "External Systems"
        Pluggy["Pluggy<br/>(Open Finance)"]
        Asaas["Asaas PSP<br/>(Webhook Events)"]
        Bank["User's Bank"]
    end

    subgraph "Fintech MVP Platform"
        subgraph "API Layer"
            WebUI["Web Dashboard<br/>(Express + EJS)"]
            APIServer["REST API<br/>(GET only)"]
        end
        
        subgraph "Processing Layer"
            WebhookReceiver["Webhook Receiver<br/>(POST /webhook/asaas)"]
            SyncDaemon["Sync Daemon<br/>(Pluggy pull + Matching)"]
        end
        
        subgraph "Data Layer"
            DB["PostgreSQL<br/>(Single DB)"]
            Redis["Redis<br/>(Session Cache)"]
        end
    end

    subgraph "User"
        Marco["Marco<br/>(PME Finance Manager)"]
    end

    %% External → Platform
    Asaas -->|Webhook: payment.received| WebhookReceiver
    Pluggy -->|API: getTransactions| SyncDaemon
    Bank -->|User connects via Pluggy| Pluggy
    
    %% Processing → Data
    WebhookReceiver -->|Write Payment rows| DB
    SyncDaemon -->|Read/Write BankTransaction| DB
    SyncDaemon -->|Match algorithm| DB
    SyncDaemon -->|Write Reconciliation/Conflict rows| DB
    
    %% Data → API
    DB -->|Query reconciliations| APIServer
    DB -->|Query conflicts| WebUI
    Redis -->|Store sessions| WebUI
    
    %% User → Platform
    Marco -->|1. Sign up + connect bank| WebUI
    Marco -->|2. Upload invoices (email/CSV)| WebUI
    Marco -->|3. View dashboard| WebUI
    Marco -->|4. Resolve conflicts| WebUI
    WebUI -->|5. See reconciled balance| Marco
    
    style WebhookReceiver fill:#e1f5ff
    style SyncDaemon fill:#f3e5f5
    style DB fill:#fff3e0
    style Redis fill:#f1f8e9
    style WebUI fill:#fce4ec
    style APIServer fill:#e0f2f1
```

## Component Interaction: Happy Path (PIX Payment)

```
Timeline: Payment flows from bank → reconciliation → dashboard

T+0s: Marco's customer sends R$ 1.000 PIX to Marco's Banco X account
  └─ Asaas detects payment in real-time
  
T+3s: Asaas sends webhook POST /webhook/asaas with payment event
  └─ WebhookReceiver:
     - Validates HMAC-SHA256 signature ✓
     - Normalizes: { amount: 1000, date: now, type: 'pix', payer_name: 'Cliente XYZ', ref_id: 'asaas-12345' }
     - Writes Payment row to DB
     - Returns 200 OK

T+5m: SyncDaemon wakes up (5min cycle), runs matching algorithm
  └─ Matching Engine:
     - Query: "Find Invoice where amount ≈ 1000 AND client ≈ 'Cliente XYZ' AND status='open'"
     - Found 1 matching invoice (NF #2024-001)
     - Create Reconciliation(payment_id=X, invoice_id=Y, status='matched')
     - Update Invoice.status = 'reconciled'
     - Update Payment.status = 'matched'

T+6m: Marco opens dashboard
  └─ WebUI renders:
     "Today: R$ 1.000 reconciled automatically ✓
      Conflicts: 0"
     - Lists Payment with status='matched', linked to Invoice #2024-001
```

## Data Model: Entity Relationships

```
┌─────────────────────────────────────────┐
│ users                                   │
├─────────────────────────────────────────┤
│ id (pk)                                 │
│ email                                   │
│ password_hash (bcrypt)                  │
│ pluggy_token (AES-256-GCM encrypted)    │
│ last_sync_at                            │
└─────────────────────────────────────────┘
         │
    ┌────┼────┬─────────────┬──────────┐
    │    │    │             │          │
    ▼    ▼    ▼             ▼          ▼
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│invoices  │ │payments  │ │recon...  │ │conflicts │
│          │ │          │ │          │ │          │
│ user_id  │ │ user_id  │ │ user_id  │ │ user_id  │
│ nf_#     │ │ amount   │ │ payment_ │ │ payment_ │
│ amount   │ │ date     │ │   id(fk) │ │   id(fk) │
│ status   │ │ type     │ │ invoice_ │ │ reason   │
│          │ │ status   │ │   id(fk) │ │          │
└──────────┘ └──────────┘ └──────────┘ └──────────┘
    ▲            ▲              │
    │            │              │
    └────────────┴──────────────┘
      1:N matching
```

## Deployment Topology (MVP)

```
┌─────────────────────────────────────────────────────────────┐
│ Single AWS EC2 t3.small (or Render, Railway, Heroku)        │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ Node.js App (npm start)                             │   │
│  │                                                     │   │
│  │  ┌────────────────┐  ┌──────────────────────────┐  │   │
│  │  │ Express Server │  │ Cron Daemons             │  │   │
│  │  │                │  │                          │  │   │
│  │  │ :3000 API+UI   │  │ - Pluggy sync (6h)      │  │   │
│  │  │ :3001 Webhook  │  │ - Matching (5min)       │  │   │
│  │  │                │  │ - Cleanup (daily)       │  │   │
│  │  └────────────────┘  └──────────────────────────┘  │   │
│  │                ▼                                    │   │
│  │  ┌──────────────────────────────────────────────┐  │   │
│  │  │ PostgreSQL Client (pg package)               │  │   │
│  │  └──────────────────────────────────────────────┘  │   │
│  │                 │                                  │   │
│  └─────────────────┼──────────────────────────────────┘   │
│                    │                                       │
│  Network           │                                       │
│  ════════════════════════════════════════════════════════  │
│                    │                                       │
│  ┌───────────────────────────────────────────────────┐   │
│  │ AWS RDS PostgreSQL (managed)                      │   │
│  │                                                   │   │
│  │ - fintech_mvp database                           │   │
│  │ - Multi-AZ (optional, for production)            │   │
│  │ - Automated backups                              │   │
│  └───────────────────────────────────────────────────┘   │
│                                                           │
│  (Optional: Redis for sessions)                         │
│  ┌────────────────────────────────────────────────────┐  │
│  │ ElastiCache Redis (or local redis-server)         │  │
│  └────────────────────────────────────────────────────┘  │
│                                                           │
└─────────────────────────────────────────────────────────────┘
```

## Security Layers

```
┌─────────────────────────────────────────────────────────┐
│ TLS/HTTPS (all external connections)                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ ┌──── User Authentication ────────────────────────┐   │
│ │ Login: email + password (bcrypt validated)      │   │
│ │ Session: cookie (httpOnly, secure flag)         │   │
│ │ API Key: hashed in DB, validated per request    │   │
│ └─────────────────────────────────────────────────┘   │
│                                                         │
│ ┌──── External System Validation ──────────────────┐  │
│ │ Asaas Webhook: HMAC-SHA256 signature verified   │  │
│ │ Pluggy Token: AES-256-GCM encrypted at rest     │  │
│ │ Database: credentials from env vars only        │  │
│ └─────────────────────────────────────────────────┘   │
│                                                         │
│ ┌──── Data Access ─────────────────────────────────┐  │
│ │ Pluggy: read-only (no payment initiation)       │  │
│ │ Asaas: webhook receiver only (no bank access)   │  │
│ │ Database: per-user row isolation (user_id fk)   │  │
│ └─────────────────────────────────────────────────┘   │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Scaling Considerations (Post-MVP)

**Single-process bottlenecks to address:**
1. Webhook receiver becomes blocking if matching takes long → split into separate process
2. Matching daemon can lag if user base grows → shard by user_id
3. DB becomes SPOF → add read replicas for API queries

**Post-MVP roadmap:**
- v1.1: Split webhook receiver into separate container
- v2.0: Message queue (RabbitMQ/SQS) for resilience; sharded daemon
- v2.5: Read replicas on database; async job processing

---

## Key Files Structure (Repo Layout)

```
.
├── src/
│   ├── server.js              ← Express app (API + dashboard)
│   ├── webhook.js             ← Asaas webhook handler
│   ├── daemon.js              ← Cron jobs (Pluggy sync + matching)
│   ├── db.js                  ← PostgreSQL connection pool
│   ├── models/
│   │   ├── user.js
│   │   ├── payment.js
│   │   ├── invoice.js
│   │   ├── reconciliation.js
│   │   └── conflict.js
│   ├── routes/
│   │   ├── api.js             ← GET /v1/*
│   │   └── dashboard.js       ← GET /, POST /resolve
│   ├── services/
│   │   ├── pluggy.js          ← Pluggy integration
│   │   ├── asaas.js           ← Asaas integration
│   │   └── matching.js        ← Matching algorithm
│   └── middleware/
│       ├── auth.js            ← Session/API key
│       └── webhook-validate.js ← HMAC validation
├── views/                      ← EJS templates
│   ├── layout.ejs
│   ├── dashboard.ejs
│   └── conflict.ejs
├── migrations/                 ← SQL schema files
│   ├── 001_initial_schema.sql
│   └── 002_indexes.sql
├── .env.example
├── package.json
└── README.md
```
