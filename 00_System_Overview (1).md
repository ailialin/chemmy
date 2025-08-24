# Master Formulation Sheet (MFS) – System Design v1.2

## 1. Purpose
Platform to manage **Master Formulation Sheets (MFS)**, products, production batches, and collaboration for cosmetic R&D and manufacturing.

Supports:
- Freelancers, small manufacturers, contract manufacturers, enterprise teams.
- Version control + approval, batch jobs (scaling, COA/SOP), multilingual (i18n).
- **Provider‑agnostic AI** (lint, INCI parser, copilot, product builder) delivered as separate phases.
- Subscription model with feature flags and usage limits.

---

## 2. Core Principles
- **Multilingual (i18n)**: every text field localized; fallback user→org→en.
- **Products ≠ MFS**: product is a commercial SKU with marketing content and pipeline; MFS is technical formulation. Product links to approved MFS version.
- **Provider‑agnostic AI**: AI Gateway abstracts vendors; RAG with strict per‑org isolation; consent‑aware data use.
- **Supabase/PostgreSQL** with Row‑Level Security; event‑driven integrations; feature flags.
- **Mobile‑first** UI and responsive design.

---

## 3. High‑Level Workflow
1) Create Draft MFS → add ingredients, steps, QC, packaging.  
2) Collaborate → comments, mentions, translations.  
3) Review & Approve → Draft → In Review → Approved → Obsolete.  
4) Link to **Product** (commercial), move along **product pipeline** (idea→launch).  
5) Create **Batch** from approved MFS → scale, checklist, COA/SOP, batch ID.  
6) Export & Share → PDFs, client review links.  
7) (Optional) AI phases → lint/parser/copilot/product builder.

---

## 4. AI Rollout Phases
- **5a**: AI Gateway, provider settings, usage logging, RAG infra.  
- **5b**: AI Lint + INCI Parser (guardrails first).  
- **5c**: AI Copilot (draft MFS, always linted).  
- **5d**: AI Product Builder (Enterprise).

---

## 5. Architecture Overview
- **Backend**: Supabase (Postgres, Auth, Storage). Service layer for API.  
- **Frontend**: React/Next.js + Tailwind.  
- **API**: REST `/api/v1`, webhooks, event bus.  
- **Integrations**: Google Drive, Slack/Telegram, n8n/Zapier, (ERP later).  
- **Observability**: metrics, structured logs, error tracking.  
- **Security**: RLS, consent flags, no‑train, tokenized shares.

---

## 6. User Segments (overview)
- Contract Manufacturers, Own Brands/R&D, Freelancers, Small Manufacturers, Enterprise.  
(See `Use_Cases.md` for details.)

---

## 7. Roadmap (excerpt)
- v1.2: Products entity, AI phases separation, consent & RAG, AI billing hooks.  
- v1.3: Copilot expansion, integrations, marketplace foundation.

---
