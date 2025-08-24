# API Design (v1.2)

**Principles:** `/api/v1`, Supabase JWT, RLS by `org_id`, i18n via `Accept-Language`, idempotency for POST, RFC7807 errors.

(Updated with: RBAC notes + 423 Locked on In Review edits, and admin endpoints prefix.)

---

## RBAC Notes
- Roles: owner, admin, qa, editor, reader (see `04_Teamwork_Workflow.md` for matrix).  
- API should return **403 Forbidden** when role lacks permission, even if RLS passes.  
- Some endpoints support Reader view-only; mutations require Admin/QA/Editor per matrix.

## In Review Lock
- Any mutation on MFS with status `in_review` MUST return **423 Locked** with problem+JSON body:  
```json
{ "type":"https://docs/errors/locked", "title":"Resource Locked", "status":423, "detail":"MFS is In Review. Reject or withdraw to edit." }
```

## Admin Endpoints
- All admin operations live under `/api/v1/admin/*` and require `super_admin` or service role.  
- Examples: `/admin/orgs`, `/admin/ai/usage`, `/admin/ai/providers`.

(For full endpoints list, see previous v1.2 section in this file.)
