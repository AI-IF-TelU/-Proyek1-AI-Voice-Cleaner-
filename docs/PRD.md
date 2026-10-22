# Product Requirements Document (draft)

## Outcome
Membantu pengguna memahami rekaman ucapan yang terganggu noise tanpa menjanjikan hasil sempurna.

## Persona
Mahasiswa yang merekam diskusi/kuliah; kreator yang merekam voiceover sederhana.

## User journey
Landing langsung ke workspace → pilih sampel atau upload → validasi → progress → hasil A/B → unduh → file dihapus sesuai retensi.

## MVP acceptance criteria
- Upload WAV dan MP3 valid; format lain ditolak dengan alasan jelas.
- Batas awal: 25 MB, durasi maksimal 120 detik (konfigurasi, perlu uji performa).
- Backend mengembalikan job ID + akses token rahasia; frontend polling status.
- Hasil dapat didengarkan dengan perbandingan waktu yang sepadan.
- Jika model gagal, tampilkan pesan aman, tidak menyimpan stack trace untuk user.
- Akses audio kedaluwarsa otomatis (target 24 jam sejak pembuatan). Penghapusan fisik dilakukan cleanup berkala dengan retry; metadata otorisasi minimal sementara mengikuti kebijakan tombstone di DATABASE_SCHEMA.md, masih tunduk persetujuan kampus.
- Aplikasi nyaman pada mobile dan desktop, keyboard accessible.

## Out of scope
Login, multi-tenant enterprise, batch upload, transkripsi, model training, live mic streaming, billing, social sharing.

## Success measures (belum ada hasil)
Job completion rate, median processing time, hasil uji intelligibility, MOS listening panel atau proxy evaluasi dengan keterbatasan dinyatakan.

## Open decisions
Rubrik Generative AI, model final, lisensi, batas durasi, lokasi deploy, kebijakan retensi, dataset evaluasi.
