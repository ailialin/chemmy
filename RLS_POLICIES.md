# Supabase RLS Policies (examples)

Ensure every multi‑tenant table has `org_id` and policies: SELECT/INSERT/UPDATE/DELETE with `org_id = auth.jwt()->>'org_id'`.
Immutable audit logs; service role only where needed.
