# Engineering Playbook (v1.2)

(Excerpt — new manual testing and accounts requirements. See `TESTING_GUIDELINES.md` for full list.)

## QA Accounts for Replit
- Create **admin test org** with users: one per role — owner, admin, qa, editor, reader.
- Create **super_admin** account for Admin Panel access.
- Seed additional Free/Pro/Team orgs to test plan limits.

## Manual Testing (high-level)
- RLS isolation across orgs.
- In Review lock: edits return **423 Locked**.
- Plan limits: Free cannot create >3 MFS (expect 402/403 with upsell), Pro limits etc.
- Admin Panel: change plan/flags; verify effect immediately.
- AI usage logging & consent gate on RAG ingestion.

See `TESTING_GUIDELINES.md` for exhaustive scenarios.
