# Admin Panel (MVP) — v1.0

**Purpose:** Separate interface for service role / `super_admin` to manage users/orgs, subscriptions, and AI diagnostics.

---

## 1) Access & Security

- **Isolation:** Admin Panel is a **separate app** (e.g., `/admin`) served only to:
  - Supabase **service role** (server-to-server) OR
  - Users with role claim `super_admin=true` in JWT.
- **Defense:** IP allowlist (optional), enforced MFA for human `super_admin`, audit every admin action.
- **RLS:** Admin Panel queries use privileged endpoints that **bypass tenant RLS** intentionally, but all mutations are **audited**.

---

## 2) Core Navigation

- **Dashboard:** quick stats (orgs/users count, plan distribution, error rate, AI usage last 24h).
- **Users & Orgs:** search, drill-down, edit plan & feature flags.
- **AI Usage:** filterable viewer over `ai_usage_log` (by org, provider, model, date).
- **AI Providers:** manage `ai_providers` (models, prices) with change history.

---

## 3) Functions (MVP)

### 3.1 Users & Organizations
- Search users by email; open user profile → linked orgs.
- Search organizations by name/domain.
- **Edit plan_tier**: Free/Pro/Team/Enterprise.
- **Edit feature_flags (jsonb)**: toggles like `ai.enabled`, `ai.rag.enabled`, `shares.client_review`.
- **Force plan refresh** (recompute flags from plan).
- **Suspend org** (soft-lock write operations).

### 3.2 Subscriptions (read-only MVP)
- View Stripe status (subscription id, renewal date, status).
- List invoices (links to Stripe).
- Manual note field (admin-only) for billing context.

### 3.3 AI Usage Monitoring
- Table over `ai_usage_log` with columns: timestamp, org, provider, model, tokens_in/out, cost_estimate, latency.
- Filters: date range, org, provider, model.
- Export CSV.

### 3.4 AI Providers Management
- CRUD for `ai_providers`: provider_name, model_id, input/output/embed costs, active.
- Bulk update costs (e.g., +10%).
- Change history (append-only log table `ai_provider_changes`).

---

## 4) API / Backend Notes

- Admin endpoints under `/api/v1/admin/*` guarded by `super_admin` claim or service role key:
  - `GET /admin/orgs`, `PATCH /admin/orgs/:id/plan`
  - `PATCH /admin/orgs/:id/feature-flags`
  - `GET /admin/ai/usage`, `GET/POST /admin/ai/providers`, `PATCH /admin/ai/providers/:id`
- All admin mutations write to `audit_logs` with `actor_role: "super_admin"`.

---

## 5) UI Considerations

- Read-only defaults; explicit “Enable edit” toggle.
- Diff preview for feature_flags JSON.
- Confirmations for destructive actions (Suspend org).
- Badges for risk: “Bypasses RLS”, “Production-impacting”.

---

## 6) Non-Goals (MVP)

- No direct data editing in core domain tables (MFS/Ingredients) — only via normal app.
- No Stripe write operations from Admin Panel (read-only links).
