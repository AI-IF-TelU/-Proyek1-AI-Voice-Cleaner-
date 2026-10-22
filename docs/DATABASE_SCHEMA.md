# PostgreSQL schema — draft

## `enhancement_jobs`
| Column | Type | Constraint / meaning |
|---|---|---|
| id | UUID | PK, generated server-side |
| access_token_hash | VARCHAR(128) | NOT NULL, hash token job |
| original_filename | VARCHAR(255) | sanitized display name |
| status | VARCHAR(16) | pending/processing/completed/failed/expired |
| input_storage_key | TEXT NULL | private storage key, not public URL |
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

## Constraints dan penghapusan (target migrasi)
Tambahkan CHECK untuk enum status, file_size_bytes > 0, durasi positif jika terisi, processing_seconds >= 0 jika terisi, serta expires_at > created_at. Validasi aplikasi tetap diperlukan.

Simpan detected_sample_rate_hz (INTEGER positif) dan detected_channels (INTEGER positif) sebagai metadata validasi decoder. Batas dukungan ditentukan setelah uji model; jangan menerima nilai tak terbatas hanya karena decoder dapat membacanya.

Saat expired, storage key boleh null setelah file berhasil dihapus. Pertahankan metadata minimal (id, access_token_hash, status, expires_at) sebagai tombstone selama 1 jam setelah expiry untuk DELETE idempotent/410, lalu hapus. Nama file dan metadata audio dibersihkan saat file dihapus. Cleanup file yang gagal harus selesai sebelum baris dihapus agar objek tidak menjadi orphan. Periode tombstone ini usulan yang masih perlu persetujuan kebijakan privasi.
