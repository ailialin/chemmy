# Teamwork & Workflow (v1.2)

**Goal:** Safe collaboration, clear responsibilities, controlled approvals.  
**Update:** Added full RBAC matrix and explicit In Review lock rules.

---

## 1) Roles & Permissions (RBAC)

| Action / Entity                                      | Owner | Admin | QA  | Editor | Reader |
|------------------------------------------------------|:-----:|:-----:|:---:|:------:|:-----:|
| Create MFS                                           |       |  ✔   |     |   ✔    |       |
| Edit MFS in **Draft**                                |       |  ✔   |     |   ✔    |       |
| Submit MFS for Review                                |       |  ✔   |     |   ✔    |       |
| Approve / Reject MFS                                 |       |  ✔   |  ✔  |        |       |
| Mark Approved → Obsolete                              |       |  ✔   |     |        |       |
| Comment / @mention                                   |       |  ✔   |  ✔  |   ✔    |  (opt)|
| View MFS (any status)                                |       |  ✔   |  ✔  |   ✔    |   ✔   |
| Create Batch (from **Approved** version only)        |       |  ✔   |  ✔  |        |       |
| Generate COA / SOP                                   |       |  ✔   |  ✔  |        |       |
| Manage Users / Roles / Billing (org-level)           |  ✔    |      |     |        |       |
| Manage Integrations                                  |  ✔    |  ✔   |     |        |       |
| Share (Client Review links)                          |       |  ✔   |  ✔  |   ✔    |       |
| Edit Products (commercial)                           |       |  ✔   |     |   ✔    |   ✔*  |

\* Reader can view products; edit only if promoted.

**Notes:**  
- Fine-grained permissions can be refined later; above is MVP baseline.  
- All mutations are checked against Supabase RLS + app-level RBAC.

---

## 2) Status Lifecycle (MFS)

- `Draft` → editable by Admin/Editor.  
- `In Review` → **locked** (no edits). Only QA/Admin can **Approve** or **Reject**.  
- `Approved` → immutable; used for Batches.  
- `Obsolete` → archived, no new batches.

### In Review — Lock Behavior
- Any attempt to edit MFS (ingredients, steps, QC, packaging, i18n) returns **HTTP 423 Locked** with message:  
  “MFS is In Review. Revert to Draft to edit (Reject or Withdraw).”
- Allowed during In Review:
  - QA/Admin: `approve`, `reject`, add **comments**.
  - Editors: **comments only** (no edits).
- After **Reject** → status `Draft`; edits allowed again, audit logged.

---

## 3) Collaboration & Audit

- Threaded comments with `field_path`, resolve/unresolve, @mentions.  
- Audit trail for all status changes and admin actions.  
- Client Review Links: tokenized, localized, optional guest comments (toggle).

---
