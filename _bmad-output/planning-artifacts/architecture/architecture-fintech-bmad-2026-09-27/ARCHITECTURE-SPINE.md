---
title: Architecture Spine — Fintech Reconciliation Platform (MVP)
status: final
created: 2026-09-27
updated: 2026-09-27
---

# Architecture Spine — Fintech Reconciliation Platform (MVP)

## Paradigm

**Event-driven, single-database microservices** — each unit (webhook receiver, sync daemon, matching engine, API server) is independently deployable and consumes or produces events through a single source-of-truth PostgreSQL database. No message queue between services; database row changes drive workflows via polling/subscribing daemons and immediate handler invocation.

This trades true decoupling for simplicity at MVP scale (single-tenant, low throughput); the database is the contract, not a service boundary.

---

## Invariants

### AD-1: Single Authoritative Database (PostgreSQL)
**Binds:** All entity data (users, integrations, invoices, payments, reconciliations, conflicts) lives in one PostgreSQL instance. No service has its own data store.

**Prevents:** Dual-write problems, eventual consistency complexity, schema divergence.

**Rule:** 
- Every micro-unit (webhook handler, sync daemon, API server) reads/writes to the same `fintech_mvp` database.
- Foreign keys and constraints enforce referential integrity at DB level.
- No caching layer except for the dashboard (Redis for session/render cache only).

**[ADOPTED]** — imposed by MVP single-tenant scope.

---

### AD-2: Webhook Receiver Is Synchronous & Stateless
**Binds:** Asaas webhook handler processes each payment event immediately, validates HMAC signature, writes to DB, and responds within 30 seconds.

**Prevents:** 
- Message loss (no intermediate queue to drop events from).
- Retry-logic complexity (Asaas will retry if we don't 200).

**Rule:**
- Handler validates webhook HMAC immediately (`HMAC(secret, body)` = header).
- Normalizes PSP event → internal `Payment` row.
- Writes to DB; if DB fails, returns 5xx (Asaas retries).
- Returns 200 only on successful DB write.
- No async job queuing; side-effects (matching, email) are daemon-driven.

**[ADOPTED]** — high-reliability requirement (RNF2 — 99.9% webhook delivery).

---

### AD-3: Pluggy Open Finance Is Read-Only, Daemon-Pulled
**Binds:** No real-time subscription to Pluggy. A scheduled daemon queries last 7 days of transactions every 6 hours; normalizes and deduplicates against existing `BankTransaction` rows.

**Prevents:**
- Webhook overload (Pluggy doesn't guarantee timeliness or order).
- Dependency on Pluggy webhook availability (we don't need it; we poll).

**Rule:**
- One Pluggy integration per user (one bank connection per account).
- Daemon: runs at 00:00, 06:00, 12:00, 18:00 UTC (or on-demand via API).
- Fetches last 7 days; applies dedup hash (`sha256(amount, date, description)`).
- Inserts or skips existing `BankTransaction` rows.
- Logs sync timestamp in `last_sync_at` for user.

**Trade-off:** 6-hour latency acceptable for MVP (NRF3 says < 60s *per sync*, not < 60s discovery); real-time would require Pluggy webhooks (enterprise feature).

---

### AD-4: Matching Engine Is Deterministic, Daemon-Driven
**Binds:** One daemon runs matching for all unreconciled payments every 5 minutes. It applies a deterministic algorithm: given a `Payment`, search `Invoice` rows by amount ± 1%, client name (fuzzy), date. If match found → create `Reconciliation` row. If no match → create `Conflict` row.

**Prevents:**
- Race conditions (single daemon).
- Unpredictable matching order (deterministic algorithm).
- Loss of conflicts (explicit row, not silent drop).

**Rule:**
- Matching algorithm:
  ```
  For each Payment P (status = 'received', not yet matched):
    invoices = Query(
      amount BETWEEN P.amount*0.99 AND P.amount*1.01,
      client_name SIMILAR TO P.payer_name (fuzzy),
      date_emitted <= P.date,
      status IN ('open', 'pending')
    )
    If invoices.length == 1:
      Create Reconciliation(payment_id, invoice_id, status='matched')
      Update Invoice.status = 'reconciled'
      Mark Payment.status = 'matched'
    Elif invoices.length > 1:
      Create Conflict(payment_id, invoice_ids, reason='ambiguous_match')
      Mark Payment.status = 'conflict'
    Else:
      Create Conflict(payment_id, null, reason='no_match')
      Mark Payment.status = 'conflict'
  ```
- Algorithm runs every 5 minutes; idempotent (won't re-match an already-matched row).
- Supports multi-payment → 1 invoice (advancements) and 1 payment → multi-invoice (splits) by allowing user manual resolution in dashboard.

---

### AD-5: API Server Is Read-Only (for MVP)
**Binds:** REST API exposes `GET` endpoints only for reconciliations, conflicts, summary. No direct payment/invoice write endpoints (writes go through webhook or daemon, not API).

**Prevents:**
- Out-of-band state mutations (all mutations go through defined flows: webhook, daemon, dashboard form).
- Consistency issues (one mutation path).

**Rule:**
- `GET /v1/reconciliations?date_from=...&date_to=...&status=matched` — list matched transactions.
- `GET /v1/conflicts` — list unmatched transactions.
- `POST /v1/conflicts/{id}/resolve` — user manually resolves (UI-driven, API layer validates).
- `GET /v1/summary` — daily/monthly rollup.
- Auth: API key in header (`X-API-Key`), validated against `ApiKey` table (hashed).
- No `POST /reconciliations` or PUT; all mutations come from webhook/daemon or dashboard (form → POST /api/conflicts/{id}/resolve).

---

### AD-6: Dashboard Is Server-Rendered, Session-Based (No SPA)
**Binds:** Web UI is a simple server-rendered application (Express + EJS or Handlebars), not a React SPA. Sessions stored in Redis or database. No JWT; simple cookie auth.

**Prevents:**
- Frontend framework complexity (MVP educacional).
- Stale data issues (direct DB-to-template rendering).

**Rule:**
- `/` (dashboard) — GET, authenticated, renders recent reconciliations + conflicts.
- `/conflicts/:id` — GET/POST, authenticated, shows detail + resolution UI.
- `/logout` — clears session.
- Session middleware validates cookie; no token refresh logic.
- CSS/JS bundled inline or static files (minimal toolchain).

**Trade-off:** No real-time updates (page refresh needed). Acceptable for MVP.

---

### AD-7: Integration Secrets & Credentials
**Binds:** Pluggy access tokens and Asaas webhook secrets are stored encrypted in DB (or env vars for Asaas secret only, since it's not per-user). Bcrypt is used for user passwords.

**Prevents:**
- Credential leakage in logs.
- Plaintext storage.

**Rule:**
- Pluggy access token: stored in `User.pluggy_token` column (encrypted with application secret key — use AES-256-GCM).
- Asaas webhook secret: stored in env var `ASAAS_WEBHOOK_SECRET` (not per-user; shared).
- User password: stored as bcrypt hash in `User.password_hash`.
- All external API calls go through SDK (Pluggy SDK, Asaas SDK).
- Logs must never include tokens or secrets; use redaction middleware.

**[ADOPTED]** — RNF1 & RNF2 (security).

---

### AD-8: Open Finance Connection Is Per-User, Scoped Read-Only
**Binds:** Each user connects their own bank account via Pluggy in onboarding. Pluggy token is stored per-user. No shared bank account.

**Prevents:**
- Multi-tenant data leakage (even though MVP is single-tenant, this keeps door open).
- Accidental write access to bank (Pluggy scope is read-only).

**Rule:**
- User → 1 Pluggy integration (1 bank connection).
- Scope: read-only, no initiation of payments.
- Token refresh handled by Pluggy SDK (or manual re-auth if expired).
- Dashboard shows "Connected to: Banco X (last sync: 6h ago)".

---

## Seed: Stack & Deployment

### Backend
- **Runtime:** Node.js 20+ (LTS), no TypeScript (keep simple, educacional).
- **Framework:** Express.js (webhook handler, API server, dashboard).
- **Database:** PostgreSQL 14+ (single instance, no replication for MVP).
- **Caching:** Redis (optional, for sessions/render caching; skip if too complex for MVP scope).
- **Scheduler:** node-cron (simple daemon tasks; no Kubernetes, just Node process).
- **Auth:** bcrypt (passwords), HMAC-SHA256 (webhook validation).

### External SDKs
- **Pluggy:** Official Node SDK (`@pluggy/sdk` or REST calls).
- **Asaas:** Official Node SDK or REST (webhook receiver + payment list API).

### Frontend
- **Server render:** Express + EJS templates (no build step, no SPA framework).
- **Styling:** Inline CSS or bootstrap CDN (keep minimal).
- **Auth:** Cookie-based sessions (express-session + Redis or connect-pg-simple).

### Deployment (MVP)
- **Single VM:** AWS EC2 t3.small or similar (or Render.com, Railway, Heroku free tier).
- **Database:** AWS RDS PostgreSQL or Render Postgres.
- **Environment:** `PGHOST`, `PGUSER`, `PGPASSWORD`, `ASAAS_WEBHOOK_SECRET`, `JWT_SECRET`, `APP_SECRET` (for encryption).
- **CI/CD:** GitHub Actions simple deploy (git push → SSH into EC2 → git pull → npm install → npm run start).
- **Monitoring:** Basic health check `/health` endpoint; logs to stdout (CloudWatch or ELK later).

---

## Data Model (Minimal)

```
users
  id (pk)
  email
  password_hash
  pluggy_token (encrypted)
  last_sync_at (Pluggy)
  created_at

integrations
  id (pk)
  user_id (fk)
  provider ('asaas', 'pluggy')
  config (JSON: merchant_id, webhook_url, etc.)
  status ('active', 'inactive')

invoices
  id (pk)
  user_id (fk)
  nf_number
  nf_date
  client_name
  amount
  status ('open', 'pending', 'reconciled')
  created_at

bank_transactions
  id (pk)
  user_id (fk)
  date
  amount
  description
  bank_code
  reference
  sync_hash (dedup)
  created_at

payments
  id (pk)
  user_id (fk)
  amount
  date
  type ('pix', 'boleto', 'ted', 'card')
  reference_id (PSP identifier)
  payer_name
  status ('received', 'matched', 'conflict')
  created_at

reconciliations
  id (pk)
  user_id (fk)
  payment_id (fk)
  invoice_id (fk)
  status ('matched', 'manual')
  created_at

conflicts
  id (pk)
  user_id (fk)
  payment_id (fk)
  invoice_ids (JSON array or string)
  reason ('no_match', 'ambiguous_match', 'value_mismatch')
  resolution (null or enum: 'linked', 'ignored', 'split')
  created_at

api_keys
  id (pk)
  user_id (fk)
  key_hash (bcrypt)
  label
  last_used_at
  created_at
```

---

## Deployment Units & Separation

All code in one git repo; three independent entry points (each a separate npm script / process type):

1. **webhook-receiver** (`npm run webhook-receiver`)
   - Express server, port 3001.
   - `POST /webhook/asaas` → validate HMAC, normalize, write DB.
   - Deployed as one container/process.

2. **sync-daemon** (`npm run sync-daemon`)
   - Node script, no HTTP server.
   - Runs cron jobs: Pluggy sync (6h), matching (5min), cleanup (daily).
   - Deployed as one container/process (or separate if scaling needed).

3. **api-web** (`npm run start`)
   - Express server, port 3000.
   - Serves dashboard UI + REST API.
   - Deployed as one container/process.

For MVP: all three run in the same process (single Node app with multiple route handlers). Later, split into separate processes if needed.

---

## Deferred

- **Multi-tenant:** Not implemented. DB schema has `user_id` on all tables to prepare; no tenant isolation logic.
- **Mobile app:** Out of scope (dashboard only).
- **Real-time notifications:** Push/email on new conflicts deferred (manual polling).
- **Advanced reporting:** Charts, exports deferred to v2.
- **Cielo/card support:** Out of MVP (Asaas PIX + boleto only).
- **Message queue (RabbitMQ, SQS):** Deferred; polling + daemon sufficient for MVP throughput.
- **Kubernetes:** Deferred (single VM sufficient).
- **TypeScript:** Deferred (keep educacional).
- **Audit logging:** Deferred (basic DB timestamp sufficient).

---

## Open Questions

- [ ] **Redis needed for MVP?** Sessions can use `connect-pg-simple` (postgres-backed sessions); skip Redis if keeping minimal.
- [ ] **Sync window:** Pluggy sync every 6h is a guess. Should it be 1h? 24h? (Validate against Pluggy rate limits + user feedback).
- [ ] **Matching tolerance (1%):** Is ±1% the right band for fee tolerance? (Validate with test data from Asaas + real invoices).
- [ ] **Fuzzy matching library:** Use `fuse.js` or `string-similarity`? (Cheap dependency; pick one at code-time).
- [ ] **Dashboard time zone:** All dates UTC or user's local time? (Assume UTC for MVP; docs clearly state this).
- [ ] **Encryption key management:** How is `APP_SECRET` (for AES-256-GCM Pluggy token) rotated? (For MVP: hardcode in env var; TODO for v1.1).
