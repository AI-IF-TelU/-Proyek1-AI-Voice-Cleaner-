# Nirava — Speech Restoration Workspace

> Nama kerja: **Nirava**. Nama ini telah digunakan pihak lain; penggunaan komersial dan ketersediaan merek/domain belum terverifikasi.
> Tagline: **Keep the voice. Lose the noise.**

## Status
Stage 1: **PIVOT TERARAH / GO tertunda**. Arsitektur disepakati, klaim Generative AI dan kesesuaian rubrik dosen belum diverifikasi. Jangan memulai Stage 2 tanpa persetujuan eksplisit.

## Problem statement
Bagaimana membersihkan rekaman percakapan yang terganggu noise sambil mempertahankan kejelasan dan karakter suara asli?

## MVP (3 fitur)
1. Unggah audio dan validasi format/durasi/ukuran.
2. Jalankan enhancement dengan status pemrosesan dan penanganan error.
3. Bandingkan audio asli/hasil secara sinkron dan unduh hasil.

## Stack
Next.js + TypeScript; FastAPI + Python; PostgreSQL; DeepFilterNet (baseline kandidat, bukan model generatif yang telah terbukti memenuhi rubrik).

## Struktur
`frontend/` UI; `backend/` API/inference; `docs/` kontrak dan keputusan; `infra/` Docker Compose PostgreSQL; `scripts/` utilitas; `tests/` tes integrasi bila diperlukan.

## Menjalankan (target, belum diimplementasikan)
1. Salin `.env.example` ke `.env` lokal; jangan commit rahasia.
2. Jalankan PostgreSQL dari `infra/compose.yaml`.
3. Instal dependensi backend dan jalankan migrasi Alembic.
4. Jalankan FastAPI dan Next.js pada terminal terpisah.
5. Periksa `/api/v1/health` dan alur upload → job → hasil.

Instruksi CLI persis akan ditambahkan setelah scaffold dibuat dan diuji.

## Audit blueprint
[Hasil audit dan audit ulang blueprint](docs/BLUEPRINT_AUDIT.md) memisahkan konsistensi rancangan dari validasi empiris. Blueprint belum membuktikan kelayakan model dan belum membuka gate Stage 2.
