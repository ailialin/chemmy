# Security Policy (v1.2)

## Data Isolation & RLS
- Per‑org RLS on all multi‑tenant tables.

## AI Data Flow
- `ai_settings.no_train` respected in provider calls.
- Consent required for training or cross‑org use; Free plan requires consent (anonymized).
- RAG isolated per org; embeddings scoped by org_id; no cross‑tenant queries.

## Secrets & Transport
- Secrets in env; rotate keys; TLS enforced; HSTS recommended.

## Logging & Privacy
- Structured logs; no PII or secrets; redact emails/tokens. Audit logs append‑only.

## Testing & Response
- SAST/DAST; dep scan; secret scan; RLS tests. Incident response with severity classes and post‑mortems.
