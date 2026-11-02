# Week 9 meta data

| Field | Raw CSV type | Silver type | Interpretation |
|---|---|---|---|
| order_id | string | string | Logical order key (corrected orders reuse the same ID); required |
| customer_id | string | string | Customer identifier; required |
| product_id | string | string | Product identifier; required |
| category | string | string | Books, Clothing or Electronics |
| unit_price | string | decimal(10,2) | Unit sale price in EUR |
| quantity | string | integer | Positive number of units |
| order_date | string | date | Order's business date |
| updated_at | string | timestamp | Timestamp for resolving corrections (all sample values use the same clock/timezone) |
| line_total | — | decimal(12,2) | Derived in Silver: `unit_price × quantity` |

**Bronze lineage columns** (added on ingestion, not in the CSV): `_source_file` (source file path, from Spark's `_metadata.file_path`), `_ingested_at` (load timestamp) and `batch_id` (`day1` or `day2`). The quarantine table has the Bronze columns plus `error_reason`.

The two order files are separate **deliveries**, not independent dimensions. `products.csv` is an optional lookup for joining/enrichment. `order_id` is unique in the Silver table, not necessarily in the Bronze deliveries.

The dataset is **synthetic**, created for the classroom; it contains no real personal information. CSV data issues are intentional.
