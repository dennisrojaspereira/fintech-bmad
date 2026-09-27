---
title: Epics and Stories — Fintech MVP
status: final
created: 2026-09-27
updated: 2026-09-27
stepsCompleted:
  - step-01-validate-prerequisites
  - step-02-design-epics
  - step-03-create-stories
inputDocuments:
  - _bmad-output/planning-artifacts/prds/prd-fintech-bmad-2026-09-27/prd.md
  - _bmad-output/planning-artifacts/architecture/architecture-fintech-bmad-2026-09-27/ARCHITECTURE-SPINE.md
---

# Epics and Stories — Fintech MVP

## Extracted Requirements

### Functional Requirements (FRs)

**Onboarding & Setup (F1)**
- FR1a: Sistema guia login via Pluggy → escolhe banco + autoriza Open Finance (read-only)
- FR1b: Usuário configura tipo(s) de documento a receber (NF-e, CSV, API)
- FR1c: Usuário escolhe 1 PSP para receber webhooks de pagamento

**Webhook Receiver (F2)**
- FR2a: Webhook receiver escuta eventos de PSP (Asaas: `payment.received`, `payment.refunded`)
- FR2b: Normaliza pra formato interno: `{ amount, date, type, reference_id, payer_name }`
- FR2c: Armazena em fila/banco de dados; valida assinatura do webhook

**Open Finance Sync (F3)**
- FR3a: Daemon executa a cada 6h → chama Pluggy API → puxa transações dos últimos 7 dias
- FR3b: Normaliza transações: `{ amount, date, description, bank_code, reference }`
- FR3c: Detecta duplicatas (mesmo hash com window de ±1h)

**Matching Engine (F4)**
- FR4a: Algoritmo: dado um pagamento recebido, busca NF com valor ≈ pagamento, cliente (fuzzy), data
- FR4b: Se achado: marca como "reconciliado"
- FR4c: Se não achado: coloca em queue de "conflitos"
- FR4d: Suporta múltiplos pagamentos → 1 NF (adiantamentos), 1 pagamento → múltiplas NFs (split)

**Dashboard (F5)**
- FR5a: Tela principal mostra total reconciliado + conflitos + lista de 50 últimas transações
- FR5b: Tela de conflitos: lista, detalhe, ações (vincular, ignorar, split)
- FR5c: Autenticação simples (usuário/senha); sem social login

**REST API (F6)**
- FR6a: `GET /v1/reconciliations` → lista com filtros (date_from, date_to, status)
- FR6b: `GET /v1/conflicts` → lista conflitos
- FR6c: `POST /v1/conflicts/{id}/resolve` → resolve manualmente
- FR6d: `GET /v1/summary` → resumo do dia/mês

### Non-Functional Requirements (NFRs)

**Security & Compliance**
- RNF1: Chaves de acesso ao Open Finance (Pluggy) armazenadas em env vars, nunca em logs
- RNF2: Senha do usuário hasheada (bcrypt), conexão HTTPS sempre
- RNF3: Webhooks de PSP validados via HMAC SHA256
- RNF4: Sem armazenamento de senha bancária (sempre via Pluggy)
- RNF5: Conformidade mínima LGPD: direito de acesso/exclusão, privacidade policy

**Performance**
- RNF6: Dashboard carrega em < 2s (p95)
- RNF7: Webhook processing < 1s (p95)
- RNF8: Matching automático roda em < 5s por 1000 transações

**Availability & Reliability**
- RNF9: 99.5% uptime (educacional)
- RNF10: Retry automático em falhas transitórias (Pluggy timeout, etc)

### Additional Requirements (Architecture & Infrastructure)

**Paradigm & Architecture**
- Event-driven architecture com single PostgreSQL database como source-of-truth
- Webhook receiver é síncrono (Asaas retries se DB falhar)
- Pluggy é daemon-polled a cada 6h (não real-time)
- Matching engine é determinístico daemon (5min interval)
- API server é read-only; todas mutations via webhook/daemon/dashboard

**Stack & Technology**
- Backend: Node.js 20+ LTS, Express.js, PostgreSQL 14+
- Optional: Redis para sessions (ou PostgreSQL-backed)
- Scheduler: node-cron (daemons)
- SDKs: Pluggy Official SDK, Asaas SDK (ou REST)
- Frontend: Server-rendered (Express + EJS), sem SPA framework

**Deployment**
- Single EC2 instance (t3.small) ou Render/Railway
- AWS RDS PostgreSQL managed
- Environment variables: PGHOST, PGUSER, PGPASSWORD, ASAAS_WEBHOOK_SECRET, APP_SECRET
- CI/CD: GitHub Actions (git push → deploy)
- Health check: `/health` endpoint

**Database Model**
- Schema: users, integrations, invoices, bank_transactions, payments, reconciliations, conflicts, api_keys
- Encryption: AES-256-GCM para Pluggy tokens
- Dedup: hash-based detection for bank transactions

**Security Implementation**
- HTTPS obrigatório
- HMAC-SHA256 validation para webhooks
- bcrypt para passwords
- Secrets management via env vars
- No logs com credentials

---

## Requirements Coverage Mapping

| Feature | FRs | NFRs | Status |
|---------|-----|------|--------|
| Onboarding | F1 (FR1a-c) | RNF2, RNF5 | Extracted |
| Webhook Receiver | F2 (FR2a-c) | RNF3, RNF7 | Extracted |
| Open Finance Sync | F3 (FR3a-c) | RNF6, RNF10 | Extracted |
| Matching Engine | F4 (FR4a-d) | RNF8 | Extracted |
| Dashboard | F5 (FR5a-c) | RNF6, RNF2 | Extracted |
| REST API | F6 (FR6a-d) | RNF1, RNF7 | Extracted |
| Infrastructure | N/A | RNF9, RNF1, RNF4 | Extracted |

---

## Epic List (APPROVED)

### Epic 1: Platform Foundation & Infrastructure
Preparar a plataforma com banco de dados, autenticação, ambiente de produção e health checks.
Users can register, login, e a plataforma está pronta pra receber integrações.
**FRs covered:** Infrastructure setup (database, env, secrets, HTTPS, health)
**NFRs covered:** RNF1, RNF2, RNF5, RNF9

### Epic 2: Bank Integration & Onboarding
Marco conecta seu banco via Pluggy e configura origem de invoices (email/CSV/API).
Users can authenticate with their bank without revealing passwords, and configure where invoices come from.
**FRs covered:** FR1a, FR1b, FR1c
**NFRs covered:** RNF2, RNF4, RNF5

### Epic 3: Payment Ingestion via Webhooks
Sistema recebe eventos de pagamento (PIX, boleto) do PSP Asaas e armazena no banco.
Users' payments are captured automatically in real-time (< 30s latency).
**FRs covered:** FR2a, FR2b, FR2c
**NFRs covered:** RNF3, RNF7

### Epic 4: Bank Statement Synchronization
Daemon sincroniza extrato bancário a cada 6h via Open Finance (Pluggy).
Users see a complete, deduplicated view of all transactions that hit their bank account.
**FRs covered:** FR3a, FR3b, FR3c
**NFRs covered:** RNF6, RNF10

### Epic 5: Automatic Reconciliation Engine
Matching daemon reconcilia automaticamente pagamentos com invoices usando algoritmo determinístico.
Users have 85%+ of payments automatically matched without manual work.
**FRs covered:** FR4a, FR4b, FR4c, FR4d
**NFRs covered:** RNF8

### Epic 6: Conflict Resolution & Dashboard
Dashboard visualiza reconciliações, mostra conflitos, permite manual resolution.
Users can see at a glance what's reconciled, identify conflicts, and resolve them with 1-2 clicks.
**FRs covered:** FR5a, FR5b, FR5c
**NFRs covered:** RNF6

### Epic 7: REST API & External Integration
API REST expõe reconciliations, conflicts, summary para ERPs e ferramentas externas.
Accountants and ERPs can pull reconciliation data programmatically.
**FRs covered:** FR6a, FR6b, FR6c, FR6d
**NFRs covered:** RNF1, RNF7

---

## FR Coverage Map (COMPLETE)

| FR | Epic |
|----|------|
| FR1a, FR1b, FR1c | Epic 2 - Bank Integration & Onboarding |
| FR2a, FR2b, FR2c | Epic 3 - Payment Ingestion |
| FR3a, FR3b, FR3c | Epic 4 - Bank Sync |
| FR4a, FR4b, FR4c, FR4d | Epic 5 - Reconciliation Engine |
| FR5a, FR5b, FR5c | Epic 6 - Dashboard & Conflict Resolution |
| FR6a, FR6b, FR6c, FR6d | Epic 7 - REST API |
| Infrastructure | Epic 1 - Foundation |

---

## Stories

### EPIC 1: Platform Foundation & Infrastructure

#### Story 1.1: PostgreSQL Database Setup & Schema Initialization
As a **DevOps Engineer**,
I want to initialize PostgreSQL with all required tables and constraints,
So that the application has a reliable source-of-truth for all data.

**Acceptance Criteria:**
- Given: Fresh PostgreSQL 14+ instance (AWS RDS or local)
- When: Running migration scripts (e.g., `001_initial_schema.sql`)
- Then: All tables (users, invoices, payments, bank_transactions, reconciliations, conflicts, api_keys, integrations) are created with correct data types and foreign keys
- And: Indexes are created on high-query columns (user_id, date, status, amount)
- And: `psql` can connect with PGHOST, PGUSER, PGPASSWORD from env vars

**Covers:** Infrastructure setup, RNF9 (uptime), RNF1 (secrets)

---

#### Story 1.2: Express.js Server Scaffolding & Health Check Endpoint
As a **Developer**,
I want to initialize an Express.js app with environment variable loading,
So that the backend has a foundation to build API endpoints and serve the dashboard.

**Acceptance Criteria:**
- Given: Node.js 20+ LTS environment
- When: Running `npm start`
- Then: Express server starts on port 3000 and logs "Server running on http://localhost:3000"
- And: `GET /health` returns `{ "status": "ok", "timestamp": "2026-09-27T..." }` with HTTP 200
- And: Environment variables (PGHOST, PGUSER, PGPASSWORD, ASAAS_WEBHOOK_SECRET, APP_SECRET) are loaded from `.env` without error
- And: Logs never leak secrets (env var values redacted in console output)

**Covers:** Infrastructure, RNF9 (health check)

---

#### Story 1.3: User Authentication System (Registration & Login)
As a **Marco (PME Finance Manager)**,
I want to register with email + password and login,
So that my account is secure and my data is private.

**Acceptance Criteria:**
- Given: User visits `/register`
- When: User enters email + password + confirms password
- Then: If passwords match, user is created in DB with bcrypt-hashed password; user is redirected to login
- And: If email already exists, error message "Email already registered" is shown
- And: Given: User visits `/login` with registered email + password
- When: User clicks "Login"
- Then: Correct credentials create a session cookie (httpOnly, secure flags set); user redirected to `/dashboard`
- And: Incorrect password shows "Invalid email or password" without revealing which field is wrong
- And: Session timeout after 24 hours of inactivity; user must re-login

**Covers:** FR (onboarding auth), RNF2 (bcrypt), RNF5 (LGPD-ready)

---

#### Story 1.4: Environment Secrets Management & Encryption Key Setup
As a **DevOps Engineer**,
I want environment variables and encryption keys stored securely,
So that tokens and passwords are never exposed in code or logs.

**Acceptance Criteria:**
- Given: Production environment (AWS EC2)
- When: `.env` file is loaded on app startup
- Then: ASAAS_WEBHOOK_SECRET and APP_SECRET are required; app fails to start if missing
- And: All external API calls never log token values (e.g., "Calling Pluggy API ***REDACTED***")
- And: Pluggy access tokens are encrypted with AES-256-GCM using APP_SECRET before storage in DB
- And: Passwords are never logged or printed; only bcrypt hashes are stored

**Covers:** RNF1 (secrets), RNF4 (no plaintext)

---

#### Story 1.5: Basic Logging & Monitoring Foundation
As a **Operations**,
I want logs written to stdout with timestamp and log level,
So that we can monitor the app in production.

**Acceptance Criteria:**
- Given: Express app running
- When: Requests come in or events occur
- Then: Logs include timestamp, level (info/warn/error), service name, and message
- And: Example: `[2026-09-27T10:30:45Z] INFO webhook-receiver: Asaas payment received for user_id=123`
- And: `/health` endpoint is logged but secrets are never in logs
- And: Error stack traces are logged for debugging but never sent to user response

**Covers:** Infrastructure, RNF9 (monitoring foundation)

---

### EPIC 2: Bank Integration & Onboarding

#### Story 2.1: Pluggy OAuth Integration & Bank Connection UI
As a **Marco**,
I want to connect my bank account via Pluggy OAuth without entering my password,
So that my bank login is secure and my data is protected.

**Acceptance Criteria:**
- Given: User is logged in and visits `/onboarding`
- When: User clicks "Connect Bank"
- Then: User is redirected to Pluggy OAuth login page (Pluggy-hosted, secure)
- And: User selects their bank (e.g., Banco X, Banco Y) and authenticates
- And: Pluggy redirects back to `/onboarding/callback?code=...`
- And: App exchanges code for Pluggy access token, stores encrypted in DB (Story 1.4)
- And: User sees "✓ Connected to Banco X" with last sync time
- And: If user declines or closes, they return to `/onboarding` with message "Bank connection cancelled"

**Covers:** FR1a, RNF4 (no password storage), RNF5 (LGPD — user controls auth)

---

#### Story 2.2: Invoice Configuration (Manual Upload via CSV)
As a **Marco**,
I want to upload a CSV of invoices to configure what to expect in payments,
So that the system knows which customers I'm billing.

**Acceptance Criteria:**
- Given: User is on `/onboarding/invoices`
- When: User uploads CSV (format: `nf_number, client_name, amount, date_emitted`)
- Then: App validates CSV format; if invalid, shows error "Invalid CSV format"
- And: If valid, parses rows and bulk-inserts into Invoice table with user_id and status='open'
- And: Shows success message "✓ Imported 15 invoices" with summary count
- And: Given: User can also choose to use email-based import (docs link)
- When: User selects "Email Integration"
- Then: Shows instructions to forward invoices to nfe+{user_id}@fintech-mvp.example.com (TODO: implement email fetcher in v1.1)
- And: Current default: "CSV upload ready; email import coming soon"

**Covers:** FR1b, RNF5 (user control)

---

#### Story 2.3: PSP Selection & Webhook Configuration
As a **Marco**,
I want to select my payment provider (Asaas) and configure webhook delivery,
So that payments are automatically sent to the platform.

**Acceptance Criteria:**
- Given: User is on `/onboarding/psp`
- When: User sees "Payment Provider" dropdown (currently: Asaas only; Cielo coming in v1.1)
- Then: User selects Asaas
- And: App generates unique webhook URL: `https://fintech-mvp.example.com/webhook/asaas/{user_id}`
- And: Shows instructions: "Copy this webhook URL into Asaas dashboard → Settings → Integrations → Webhooks"
- And: User can test webhook by clicking "Test Webhook" (dummy payment event)
- And: Shows success "✓ Asaas webhook configured" once a test event is received

**Covers:** FR1c, FR2a (webhook setup)

---

#### Story 2.4: Onboarding Completion & First Login
As a **Marco**,
I want to finish onboarding and see my dashboard,
So that I'm ready to start reconciling payments.

**Acceptance Criteria:**
- Given: User has completed all onboarding steps (auth, bank, invoices, PSP)
- When: User clicks "Complete Onboarding" on summary page
- Then: User is marked as onboarded=true; profile is created
- And: User is redirected to `/dashboard`
- And: Dashboard shows: "Welcome, Marco! 0 reconciliations today. 0 conflicts."
- And: User can click "Settings" to re-edit any onboarding step (Pluggy token, invoices, PSP)

**Covers:** FR1a/b/c (onboarding complete)

---

### EPIC 3: Payment Ingestion via Webhooks

#### Story 3.1: Asaas Webhook Receiver & Signature Validation
As a **Webhook Handler**,
I want to receive payment events from Asaas and validate the signature,
So that fake payment events can't fool the system.

**Acceptance Criteria:**
- Given: Asaas sends `POST /webhook/asaas/{user_id}` with body and `X-Asaas-Signature` header
- When: Webhook handler receives request
- Then: Handler extracts ASAAS_WEBHOOK_SECRET from env vars
- And: Computes HMAC-SHA256(body, secret); compares with X-Asaas-Signature header
- And: If signatures match: continues processing; if not: returns HTTP 403 Forbidden, logs "Invalid signature"
- And: Invalid request is logged but NOT stored in DB

**Covers:** FR2a, RNF3 (webhook validation)

---

#### Story 3.2: Payment Event Normalization & Storage
As a **Payment Receiver**,
I want to extract payment data from Asaas and store it in standard format,
So that the reconciliation engine can process any payment consistently.

**Acceptance Criteria:**
- Given: Valid Asaas webhook (Story 3.1) with event_type in [payment.received, payment.refunded]
- When: Event body contains: { amount, date, payment_method, payer_name, reference_id, status }
- Then: Handler normalizes to internal schema: `{ amount, date, type, reference_id, payer_name }`
  - Mapping: `payer_name` from Asaas customer name; `type` = payment_method (pix/ted/boleto/card); `reference_id` = Asaas txn_id
- And: Creates Payment row in DB with status='received'
- And: Returns HTTP 200 OK (tells Asaas "got it, don't retry")
- And: If DB write fails: returns HTTP 5xx (Asaas will retry)

**Covers:** FR2b, FR2c

---

#### Story 3.3: Duplicate Payment Detection
As a **Payment Handler**,
I want to detect and skip duplicate payment events,
So that the same payment isn't recorded twice.

**Acceptance Criteria:**
- Given: Payment is received and normalized (Story 3.2)
- When: Handler checks if Payment with same (user_id, reference_id, amount, date) exists within last 24h
- Then: If exact match found: skips insert, returns HTTP 200 (idempotent — Asaas is happy)
- And: If no match: inserts new Payment row
- And: Logs duplicate: "Skipped duplicate payment asaas-txn-12345 for user_id=X"

**Covers:** FR2c (reliability)

---

### EPIC 4: Bank Statement Synchronization

#### Story 4.1: Pluggy API Integration & Transaction Fetch
As a **Sync Daemon**,
I want to fetch the last 7 days of transactions from the user's bank via Pluggy,
So that we have all deposits and transfers recorded.

**Acceptance Criteria:**
- Given: Daemon task scheduled to run every 6 hours
- When: Task executes (e.g., 00:00, 06:00, 12:00, 18:00 UTC)
- Then: For each user with pluggy_token:
  - Pluggy SDK authenticates with user's token
  - Fetches transactions for date_from = today - 7 days, date_to = today
  - Returns list: [ { amount, date, description, bank_code, reference }, ... ]
- And: If Pluggy API fails (timeout/error): logs warning, skips user, continues with next
- And: After successful fetch: updates User.last_sync_at = now

**Covers:** FR3a, RNF10 (retry on fail)

---

#### Story 4.2: Bank Transaction Normalization & Deduplication
As a **Sync Daemon**,
I want to normalize bank transactions and skip duplicates,
So that the reconciliation engine sees only unique, clean data.

**Acceptance Criteria:**
- Given: Transactions fetched from Pluggy (Story 4.1)
- When: For each transaction, daemon computes dedup_hash = SHA256(amount + date + description)
- Then: Checks if BankTransaction with same (user_id, dedup_hash) exists (within ±1h window)
- And: If exists: skips (duplicate)
- And: If new: normalizes to schema { amount, date, description, bank_code, reference, dedup_hash, sync_hash }
  - Stores in BankTransaction table with status='synced'
- And: Logs summary: "Synced 12 transactions; skipped 2 duplicates"

**Covers:** FR3b, FR3c (dedup)

---

#### Story 4.3: Bank Sync Monitoring & Error Handling
As a **Operator**,
I want to see if bank sync succeeded and handle failures gracefully,
So that data gaps don't surprise us.

**Acceptance Criteria:**
- Given: Daemon runs every 6h
- When: Sync completes (success or failure)
- Then: Result logged: "Bank sync for user_id=X: 12 new, 2 dupes, 0 errors" (success)
- And: If Pluggy API timeout: logs "Bank sync for user_id=X: timeout, will retry at next cycle"
- And: Dashboard shows "Last sync: 30 min ago ✓" or "Last sync: 3 hours ago ⚠️ (retry pending)"
- And: No data is lost; failed users are retried in next cycle

**Covers:** RNF6, RNF10 (monitoring)

---

### EPIC 5: Automatic Reconciliation Engine

#### Story 5.1: Matching Algorithm Implementation (Core Logic)
As a **Matching Engine**,
I want to implement the deterministic matching algorithm,
So that payments are automatically linked to invoices.

**Acceptance Criteria:**
- Given: A Payment (status='received') and list of Invoices (status='open')
- When: Daemon runs matching algorithm (every 5 min)
- Then: For each unmatched Payment:
  - Query Invoices where:
    - amount BETWEEN Payment.amount * 0.99 AND Payment.amount * 1.01 (±1% tolerance)
    - client_name SIMILAR TO Payment.payer_name (fuzzy, using fuse.js or similar)
    - date_emitted <= Payment.date
    - status IN ('open', 'pending')
  - If exactly 1 match: return it
  - If 0 matches: return null
  - If >1 matches: return multiple (ambiguous)
- And: Algorithm is deterministic (same input = same output every time)
- And: Runs idempotent (won't re-match already-matched rows)

**Covers:** FR4a

---

#### Story 5.2: Reconciliation Record Creation & Status Update
As a **Matching Engine**,
I want to create Reconciliation records and update Invoice/Payment status,
So that we know what's been matched.

**Acceptance Criteria:**
- Given: Matching algorithm finds a match (Story 5.1)
- When: Creates Reconciliation row: { user_id, payment_id, invoice_id, status='matched', created_at }
- Then: Updates Invoice.status = 'reconciled'
- And: Updates Payment.status = 'matched'
- And: Both records are linked and immutable (no future updates)
- And: Logs: "Matched payment_id=123 to invoice_id=456 (Marco's Consultoria, R$ 1.000)"

**Covers:** FR4b

---

#### Story 5.3: Conflict Record Creation (No Match / Ambiguous)
As a **Matching Engine**,
I want to identify and record unmatched or ambiguous payments,
So that Marco can manually resolve them.

**Acceptance Criteria:**
- Given: Matching algorithm finds 0 or multiple matches (Story 5.1)
- When: Creates Conflict row: { user_id, payment_id, invoice_ids (JSON), reason, resolution=null }
  - reason = 'no_match' (0 matches) or 'ambiguous_match' (>1 matches)
- Then: Updates Payment.status = 'conflict'
- And: Conflict is stored for manual review in dashboard (Story 6)
- And: Logs: "Conflict created: payment_id=123, reason=no_match"

**Covers:** FR4c

---

#### Story 5.4: Split & Multi-Payment Scenarios
As a **Matching Engine**,
I want to support split payments (1 invoice matched by multiple payments) and advancements,
So that complex reconciliation is possible.

**Acceptance Criteria:**
- Given: Two payments totaling R$ 1.000 for one invoice of R$ 1.000
- When: Manual resolution UI (Story 6.2) allows user to click "Link This Payment" on multiple payments to same invoice
- Then: Creates multiple Reconciliation rows (one per payment) with same invoice_id
- And: Invoice.status remains 'reconciled' after first payment, additional payments don't change it
- And: Given: One payment of R$ 1.500 split across two invoices (R$ 1.000 + R$ 500)
- When: User manually links this payment to both invoices in proportions
- Then: Creates Reconciliation_Detail rows (or flags for future audit) marking split allocation

**Covers:** FR4d (advanced matching)

---

### EPIC 6: Conflict Resolution & Dashboard

#### Story 6.1: Dashboard Main View (Reconciliation Summary)
As a **Marco**,
I want to see a summary of today's reconciliations at a glance,
So that I know how much work is done and how much remains.

**Acceptance Criteria:**
- Given: User logged in, visits `/dashboard`
- When: Page loads
- Then: Shows summary card:
  - "Today: R$ XX.XXX reconciled ✓" (sum of matched Payments.amount for today)
  - "Y conflicts ⚠️" (count of Conflicts with resolution=null)
  - Last sync time: "Bank updated 30 min ago"
- And: Below, shows table of last 50 transactions:
  - Columns: Date | Amount | Client | Type (PIX/Boleto/Card) | Status (OK/Conflict) | Action
- And: Sorting by date DESC (most recent first)
- And: Clicking row expands details (invoice matched, payer name, reference)

**Covers:** FR5a

---

#### Story 6.2: Conflict Resolution UI (Manual Linking)
As a **Marco**,
I want to manually resolve conflicts by linking payments to different invoices,
So that exceptions can be fixed without developer help.

**Acceptance Criteria:**
- Given: User clicks on a Conflict row (status='conflict')
- When: Page navigates to `/conflicts/{conflict_id}`
- Then: Shows conflict detail:
  - Payment: "R$ 1.000 from Customer XYZ on 2026-09-27"
  - Reason: "no_match" or "ambiguous_match"
  - If ambiguous: list candidate invoices with fuzzy match score
- And: User can:
  - Click "Ignore" (marks resolution='ignored', payment stays 'conflict', no change)
  - Click "Link to Invoice" (shows searchable invoice list, user picks one, creates Reconciliation, updates statuses)
  - Click "Mark as Advance" (creates Reconciliation with flag 'advance', updates Invoice to 'pending' not 'reconciled')
- And: After action, page shows "✓ Resolved" and redirects to `/dashboard`

**Covers:** FR5b

---

#### Story 6.3: Dashboard Responsiveness (Desktop & Tablet)
As a **Marco**,
I want the dashboard to work on my laptop and tablet,
So that I can check reconciliation status anywhere.

**Acceptance Criteria:**
- Given: Dashboard served by Express + EJS (server-rendered, not SPA)
- When: Viewport width 320px (mobile): layout stacks vertically
  - Table becomes card-based (one transaction per card)
  - Actions are visible and clickable
- And: Viewport width 768px (tablet): two-column layout
  - Summary cards on left, table on right
  - Text remains readable, images/icons scale
- And: Viewport width 1024px+ (desktop): full layout
- And: No horizontal scroll; all content visible without pinch-zoom

**Covers:** RNF6 (responsiveness, < 2s load)

---

#### Story 6.4: Dashboard Performance (< 2s Load Time)
As a **Operations**,
I want the dashboard to load in < 2 seconds (p95),
So that Marco isn't frustrated by slowness.

**Acceptance Criteria:**
- Given: User with 1000+ transactions in DB
- When: `/dashboard` is loaded (cold cache, no Redis)
- Then: Page renders in < 2s (p95 latency)
- And: Database query is optimized (indexed on user_id, date, status)
- And: EJS template renders in < 100ms
- And: CSS/JS is minimal (no large frameworks; inline where possible)
- And: Monitoring via `/metrics` endpoint tracks page load time

**Covers:** RNF6 (performance)

---

### EPIC 7: REST API & External Integration

#### Story 7.1: GET /v1/reconciliations Endpoint
As a **ERP or Accounting Software**,
I want to fetch reconciled transactions via REST API,
So that I can import reconciliation data into my system.

**Acceptance Criteria:**
- Given: API client with valid API key
- When: `GET /v1/reconciliations?date_from=2026-09-01&date_to=2026-09-30&status=matched`
- Then: Returns JSON array of Reconciliation records:
  ```json
  [
    {
      "id": "recon-123",
      "payment_id": "pay-456",
      "invoice_id": "inv-789",
      "amount": 1000.00,
      "date": "2026-09-27",
      "status": "matched"
    }
  ]
  ```
- And: Supports filters: date_from, date_to, status (matched/conflict/ignored)
- And: Supports pagination: page=1, limit=100 (default 50, max 500)
- And: Rate limit: 1000 requests/minute per API key

**Covers:** FR6a

---

#### Story 7.2: GET /v1/conflicts Endpoint
As a **ERP**,
I want to fetch unresolved conflicts via API,
So that I can alert the user or auto-resolve via my own logic.

**Acceptance Criteria:**
- Given: API client with valid API key
- When: `GET /v1/conflicts?resolution=null&limit=50`
- Then: Returns JSON array of Conflict records with details:
  ```json
  [
    {
      "id": "conf-123",
      "payment": { "id": "pay-456", "amount": 1000, "date": "2026-09-27", "payer_name": "XYZ" },
      "invoice_ids": ["inv-789", "inv-790"],
      "reason": "ambiguous_match",
      "resolution": null
    }
  ]
  ```
- And: Filters: resolution (null/ignored/linked), date_from, date_to

**Covers:** FR6b

---

#### Story 7.3: POST /v1/conflicts/{id}/resolve Endpoint
As a **ERP**,
I want to programmatically resolve a conflict,
So that automated workflows can clear exceptions.

**Acceptance Criteria:**
- Given: API client with valid API key
- When: `POST /v1/conflicts/conf-123` with body:
  ```json
  {
    "action": "link",
    "invoice_id": "inv-789"
  }
  ```
- Then: Creates Reconciliation row (payment_id, invoice_id)
- And: Updates Conflict.resolution = 'linked'
- And: Returns HTTP 200 with updated Conflict
- And: Supports actions: "link" (to invoice_id), "ignore" (sets resolution='ignored'), "split" (complex, docs needed)

**Covers:** FR6c

---

#### Story 7.4: GET /v1/summary Endpoint & Daily Metrics
As a **Dashboard (or External Reporter)**,
I want to fetch daily/monthly reconciliation summary,
So that we can show KPIs and trend data.

**Acceptance Criteria:**
- Given: API client requests `GET /v1/summary?period=day&date=2026-09-27`
- When: Endpoint executes
- Then: Returns JSON summary:
  ```json
  {
    "date": "2026-09-27",
    "total_received": 25000.00,
    "reconciled": 21250.00,
    "conflict_count": 3,
    "match_rate": 0.85,
    "avg_resolution_time_minutes": 15
  }
  ```
- And: Supports period: "day", "week", "month"
- And: Caches result for 5 minutes (Redis or in-memory)

**Covers:** FR6d

---

#### Story 7.5: API Key Management & Authentication
As a **Marco**,
I want to create and revoke API keys,
So that external systems can access my reconciliation data securely.

**Acceptance Criteria:**
- Given: User visits `/settings/api-keys`
- When: User clicks "Create API Key"
- Then: Generates new random key (64 hex chars), displays it once, stores bcrypt hash in DB
- And: User can label the key ("Omie Integration", "Accountant Dashboard", etc.)
- And: User can revoke a key (deletes it, invalidates all requests with that key)
- And: Each request with API key is logged (not the key value): "API request from key 'abc...xyz' at 2026-09-27 10:30:45"
- And: All API endpoints validate key in `X-API-Key` header against bcrypt-hashed values

**Covers:** FR6 (all), RNF1 (security)
