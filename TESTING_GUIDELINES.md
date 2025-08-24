# Testing Guidelines (v1.0)

Comprehensive manual + automated test scenarios.

---

## 1) Test Accounts & Data

- **Admin Panel access:** create `super_admin` user with MFA (or service role key).  
- **Per-role users** in a seeded org: `owner`, `admin`, `qa`, `editor`, `reader`.
- **Plan variants:** one org per plan (Free, Pro, Team) for limit checks.
- Seed 20+ MFS (various statuses), 5 products, ingredient prices, and a few batches.

---

## 2) RBAC Scenarios

- **Editor** can create/edit Draft, submit for review; cannot approve/reject.  
- **QA** can approve/reject; cannot edit Draft unless also Admin.  
- **Reader** can view and comment (if allowed), but never mutate.  
- **Owner** manages billing/roles.  
- API must return **403** when role lacks permission.

---

## 3) In Review Lock

- Put MFS into `In Review`.  
- Try to edit ingredients/steps/QC: expect **423 Locked**.  
- Add comments: allowed.  
- Reject → Draft: edits become possible again.

---

## 4) Plan Limits

- **Free**: attempt to create 4th MFS → expect error/upsell.  
- **Pro**: create up to 100 MFS; verify quotas for AI calls (e.g., 50/month).  
- Verify feature flags toggle UI (Client Review links disabled on Free).

---

## 5) AI Usage & Consent

- Run `/ai/lint` and `/ai/copilot` actions; verify `ai_usage_log` entries (tokens, cost).  
- Attempt RAG ingest with consent=false → expect rejection.  
- Toggle consent=true → ingest permitted.

---

## 6) Admin Panel

- Update org `plan_tier` and individual `feature_flags`; verify immediate effect.  
- Edit `ai_providers` price; run AI call → cost uses new tariff.  
- Export AI usage CSV filtered by org/date.

---

## 7) E2E Happy Paths

- Create MFS → submit → approve → create batch → generate COA/SOP → share link.  
- Create Product, link Approved MFS version; export product description.

---

## 8) Performance

- Seed 10k MFS; search p95 < 300ms; verify pagination and indexes.  
- Batch scaling math error ≤ 0.1% across random targets.

---

## 9) Security

- RLS bypass attempts across orgs fail.  
- Share links respect expiry/password.  
- No secrets/PII in logs.
