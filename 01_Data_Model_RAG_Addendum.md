# Data Model Addendum — RAG Types (v1.2)

- `rag_documents.document_type` must be one of: `mfs`, `product`, `sop`, `coa`, `attachment`.  
- `reference_id` points to the source record (MFS id, product id, file id).  
- Text extraction for PDFs (SOP/COA) stored in a normalized form before embedding.  
- Isolation by `org_id` is mandatory; cross-tenant retrieval is forbidden.
