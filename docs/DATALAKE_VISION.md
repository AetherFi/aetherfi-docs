# 📂 Datalake Vision: Future ETL & Hybrid Retrieval for AetherFi

## 🧠 Purpose

The datalake acts as a raw, unstructured staging layer—ideal for ingesting logs, HTML files, CI failures, and external signals (e.g. StackOverflow, Reddit).

This enables future ETL → Qdrant vectorization → RAG or RAR queries.

---

## 🛠️ Planned Tooling

| Tool            | Use Case                        |
|-----------------|----------------------------------|
| BeautifulSoup   | Scrape + chunk HTML/Reddit      |
| Pandas / Polars | Transform logs to dataframes    |
| SQLAlchemy      | Store metadata in Postgres      |
| Qdrant client   | Push chunk embeddings           |
| Alembic         | DB schema versioning            |

---

## 🗃️ Sample Schema

```sql
id | source_type | tags     | chunk_id | vector_id | created_at
---|-------------|----------|----------|-----------|------------
1  | html        | triage   | x001     | 9fj21...  | 2025-06-01
