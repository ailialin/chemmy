# Cosmetics MFS Platform – Design Docs (v1.2)

## Files (key)
- `00_System_Overview.md` — Overview, flows, AI rollout
- `01_Data_Model.md` — Schema (incl. Products, AI). See also: `01_Data_Model_RAG_Addendum.md` for RAG types.
- `02_API_Design.md` — REST v1; now includes RBAC/423 lock note; admin endpoints.
- `03_UI_UX.md` — Screens & patterns
- `04_Teamwork_Workflow.md` — **RBAC matrix** + In Review lock rules (423)
- `05_Billing_Subscription.md` — Plans, AI quotas, consent
- `06_AI_Features.md` — **INCI Parser & Copilot examples**, RAG sources & guardrails
- `07_Integrations.md` — Integrations & event bus
- `08_Admin_Panel.md` — **Admin interface (MVP)** for super_admin/service role
- `Use_Cases.md` — Segments, use cases, features
- `ENGINEERING_PLAYBOOK.md` — Phases, ops, **manual testing excerpt**
- `TESTING_GUIDELINES.md` — **Full manual testing scenarios**
- `SECURITY.md`, `CONTRIBUTING.md`, `CODING_STANDARDS.md`, `RLS_POLICIES.md`

## What changed in this update
- Added **Admin Panel** spec.
- Formalized **RBAC matrix** and **In Review lock** behavior.
- Expanded **AI features** with concrete examples and **RAG document types**.
- Added **Testing Guidelines** + requirement to seed accounts for each role and `super_admin`.

