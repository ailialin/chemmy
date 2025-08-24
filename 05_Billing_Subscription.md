# Billing & Subscription Model (v1.2)

## Plans (excerpt)
- **Free**: 3 MFS / 1 product; AI disabled *unless consent=true* (limited); PDFs only; no shares.
- **Pro**: 100 MFS / 10 products; AI Lint incl.; Copilot 50 calls/mo; Costing; no RAG without consent.
- **Team**: Unlimited; AI Lint+Copilot 500/mo; AI Translate; limited RAG (with consent); Slack/Drive.
- **Enterprise**: Unlimited; Product Builder; dedicated provider; on‑prem S3/RAG; custom SLA.

## AI Billing
- Usage logged in `ai_usage_log`; pricing from `ai_providers`.
- Plan quotas → overage billed or blocked.
- `/billing/ai` shows usage & forecast.

## Consent
- Free requires consent to anonymized data use; `ai_settings.consent_data_use=true`.
- Data anonymization pipeline mandatory.
