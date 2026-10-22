# API Contract — v1 draft

Base path `/api/v1`; JSON errors `{ "code": "...", "message": "..." }`. Seluruh operasi job memakai token akses rahasia pada header `X-Job-Token`, dikirim hanya ke pemilik sesi browser; tidak masuk URL atau log.

## `GET /health`
200 `{ "status": "ok" }` (jangan tampilkan secrets atau detail infrastruktur).

## `POST /enhancements`
`multipart/form-data` dengan field `file`. 202:
```json
{"job_id":"uuid","job_token":"random-secret","status":"pending"}
```
400/413/415/422 untuk input tidak valid, 429 untuk batas konkurensi.

## `GET /enhancements/{job_id}`
Header `X-Job-Token`. 200:
```json
{"job_id":"uuid","status":"processing","duration_seconds":12.4,"processing_seconds":null,"error":null}
```
Status: `pending | processing | completed | failed | expired`.

## `GET /enhancements/{job_id}/audio?version=original|enhanced`
Header `X-Job-Token`; stream audio; enhanced hanya tersedia setelah completed. Gunakan cache-control private/no-store; jangan ekspos path disk.

## `DELETE /enhancements/{job_id}`
Header `X-Job-Token`; hapus audio dan tandai job expired. Respons 204; operasi idempotent.

## Security/limits
CORS allowlist eksplisit, request size limit pada reverse proxy dan API, rate limit, MIME + magic/decoder verification, UUID opaque, token di-hash pada DB, tidak simpan token plaintext. Pembersihan file pada error dan expiry.
