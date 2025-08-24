# Data Model & Multilingual Support (v1.2)

## 1. Organizations & Users
- **orgs**: id, name, default_locale, plan_tier, feature_flags jsonb, billing_customer_id, created_at
- **users**: id, email (Auth), preferred_locale, preferred_units, timezone, created_at
- **user_orgs**: user_id, org_id, role (owner, admin, qa, editor, reader)

## 2. i18n Principle
- Base tables store IDs/numerics; localized fields in `<entity>_i18n(locale, …)` with status `draft/machine/human_reviewed`.
- Fallback: user→org→en.

## 3. MFS & Versioning
- **mfs**: id, org_id, default_locale, category_id, status (draft/in_review/approved/obsolete), created_by, created_at, updated_at
- **mfs_i18n**: mfs_id, locale, product_name, short_description, tags text[]
- **mfs_versions**: id, mfs_id, version_code, is_latest, base_version_id, created_by, created_at, changes_summary jsonb, commit_message text

## 4. Ingredients
- **ingredients**: id, org_id, inci_name, cas_number, category_id
- **ingredients_i18n**: ingredient_id, locale, display_name, function_label, notes, status
- **ingredient_prices**: id, ingredient_id, supplier_id, volume_tier, unit_price, currency, valid_from

## 5. Equipment & Packaging
- **equipment**: id, org_id, type, capacity_kg, volume_min_ml, volume_max_ml, precision
- **equipment_i18n**: equipment_id, locale, display_name, attachment_types, cleaning_instructions
- **materials**: id, name
- **packaging_options**: id, org_id, material_id, volume_ml, sku_code
- **packaging_options_i18n**: packaging_id, locale, container_type, cap_type, marketing_notes

## 6. QC & Approvals
- **qc_parameters**: id, org_id, param_type, target_value, acceptable_min, acceptable_max, method_id, frequency, sampling, micro_limits
- **qc_parameters_i18n**: qc_id, locale, display_name, notes
- **approvals**: id, entity_type, entity_id, from_status, to_status, approved_by, approved_at, note
- **comments**: id, entity_type, entity_id, field_path, locale, author_id, message, created_at
- **audit_logs**: id, org_id, actor_id, action, entity_type, entity_id, diff jsonb, created_at

## 7. Batches & Documents
- **batches**: id, org_id, mfs_id, mfs_version_id, target_quantity, unit, status (planned/in_progress/completed), executed_at, created_by
- **coa**: id, batch_id, locale, pdf_url, created_at
- **sop**: id, mfs_id or batch_id, locale, pdf_url, created_at

## 8. Billing & Usage
- **billing_subscriptions**: org_id, provider, customer_id, product_id, price_id, status, current_period_end
- **usage_counters**: org_id, period, key, value

## 9. Products (NEW)
- **products**: id, org_id, product_code, status (idea, techsheet, sample, packaging, launched), current_mfs_version_id, created_at, updated_at
- **product_i18n**: product_id, locale, display_name, description, marketing_claims, status, updated_at

## 10. AI (NEW)
- **ai_providers**: id, provider_name (openai, anthropic, azure, google, self_hosted), model_id, input_cost_per_1k, output_cost_per_1k, embed_cost_per_1k, active
- **ai_usage_log**: id, org_id, provider_id, model_id, tokens_in, tokens_out, cost_estimate, latency_ms, created_at
- **ai_settings**: id, org_id, provider_id, model_id, rag_enabled, consent_data_use, no_train, feature_flags jsonb, updated_at
- **rag_documents**: id, org_id, document_type (mfs, product, attachment), reference_id, embedding (vector), locale, created_at

**Notes:** Per‑org RAG isolation; consent gates ingestion of client data; versions/audits append‑only.
