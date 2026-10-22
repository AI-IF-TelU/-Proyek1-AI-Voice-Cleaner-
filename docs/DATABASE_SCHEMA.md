# PostgreSQL schema — draft

## `enhancement_jobs`
| Column | Type | Constraint / meaning |
|---|---|---|
| id | UUID | PK, generated server-side |
| access_token_hash | VARCHAR(128) | NOT NULL, hash token job |
| original_filename | VARCHAR(255) | sanitized display name |
| status | VARCHAR(16) | pending/processing/completed/failed/expired |
| input_storage_key | TEXT | private storage key, not public URL |
| output_storage_key | TEXT NULL | enhanced audio key |
| content_type | VARCHAR(100) | detected MIME |
| file_size_bytes | BIGINT | positive |
| duration_seconds | DOUBLE PRECISION NULL | validated duration |
| processing_seconds | DOUBLE PRECISION NULL | runtime |
| error_code | VARCHAR(64) NULL | safe error category |
| created_at | TIMESTAMPTZ | default now() |
| started_at | TIMESTAMPTZ NULL | processing start |
| completed_at | TIMESTAMPTZ NULL | completion |
| expires_at | TIMESTAMPTZ | indexed for cleanup |

Indexes: `(status, created_at)`, `(expires_at)`. Alembic migrations as source of truth.

## Retention
Target 24h, adjustable after privacy requirements. Cleanup process deletes storage objects and metadata or retains only aggregate anonymized counters with explicit policy. Prevent stale paths and orphan files.

## No user table initially
MVP tanpa akun. Job token adalah capability credential; tetap ada risiko jika token bocor. Jangan simpan audio bytes di PostgreSQL.
