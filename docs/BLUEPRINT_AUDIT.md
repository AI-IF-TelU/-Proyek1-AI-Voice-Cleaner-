# Audit blueprint - 23 Oktober 2026

## Verdict
**Dokumentasi lebih konsisten; Stage 1 tetap PIVOT TERARAH / GO tertunda.** Belum layak dinyatakan tervalidasi secara empiris. Tidak ada kode Stage 2 yang dibuat melalui audit ini.

## Cakupan dan metode
Pemeriksaan statis README, PRD, Stage 1, arsitektur, API, skema, desain, pengembangan, evaluasi, env template, dan aturan Git. Audit ini tidak mencakup riset eksternal, pemeriksaan lisensi aktual, eksekusi model, benchmark, atau persetujuan dosen. Angka batas upload/retensi masih target rancangan.

## Temuan dan perbaikan
| Temuan | Risiko | Tindakan dokumentasi |
|---|---|---|
| Token diwajibkan untuk seluruh operasi, termasuk sebelum job dibuat | Kontrak create ambigu | Pengecualian POST, token kriptografis sekali kirim dan no-store |
| Respons auth, expiry, dan audio belum terdefinisi | FE/BE berbeda perilaku | 404 seragam, 410 tombstone, 409 hasil belum tersedia, envelope error |
| Header token tidak dapat dipasang langsung pada elemen audio | Playback/download tidak bekerja | Fetch berheader dan object URL |
| DELETE saat inference dan cleanup belum rinci | Hasil muncul lagi atau file orphan | Transisi expired atomik, output terlambat dihapus, retry cleanup |
| Sample rate/channel belum tercakup | Beban decoder dan input model tidak terkontrol | Metadata dan batas decoder/model diwajibkan; angka menunggu uji |
| Exception fixtures membuka izin audio/weights | Berkas pribadi ikut Git | Hapus exception luas; tambah ignore env/runtime/weights/dump |

## Hal yang sudah selaras
- MVP upload -> enhancement -> A/B + download; tanpa akun, billing, Redis/Celery, dan Three.js.
- Next.js hanya mengakses FastAPI; inference backend; PostgreSQL metadata dan storage audio privat.
- UUID bukan otorisasi; token hash; migrasi Alembic sebagai sumber skema.
- DeepFilterNet hanya kandidat baseline; tidak dinyatakan memenuhi Generative AI.
- UI dan evaluasi melarang metrik/hasil fiktif serta mengakui batasan.

## Bukti wajib sebelum GO
1. Rubrik resmi dan keputusan apakah model generatif diwajibkan.
2. Model final, lisensi model/dependensi/data, serta justifikasi ilmiah sesuai rubrik.
3. Uji 3-5 audio berizin: intelligibility/artifacts, runtime, memori, sample rate/channel, batas input dan biaya perangkat/deploy.
4. Riset kompetitor dan validasi target; studi pemenang hanya bila relevan dengan mata kuliah/acara.
5. Kebijakan server/retensi termasuk tombstone, format hasil, dan batas dukungan audio yang disetujui.
6. Verdict GO berbukti serta persetujuan eksplisit pengguna atas demo concept.

## Verifikasi audit
Pemeriksaan diff/whitespace dan daftar file staging dilakukan sebelum commit. Tidak ada tes API/audio, lint, atau typecheck yang dapat dijalankan karena repository masih berisi blueprint tanpa scaffold. Seluruh perilaku teknis yang ditambahkan adalah spesifikasi target, belum bukti implementasi.

## Audit ulang terhadap commit 56ceba3
Audit ulang menemukan bahwa sebagian perbaikan yang disebut laporan sebelumnya sudah tidak ada pada dokumen aktif. Kontrak tersebut dipulihkan sambil mempertahankan identitas Nirava. Laporan sebelumnya bukan bukti bahwa versi terbaru sudah memenuhi seluruh rekomendasi.

| Prioritas | Temuan tambahan | Perbaikan target |
|---|---|---|
| Tinggi | DELETE 204 dianggap sudah menghapus bytes walau worker masih berjalan | Bedakan pencabutan akses atomik dan cleanup fisik dengan retry |
| Tinggi | Recovery startup dapat menggagalkan worker proses lain | Tegaskan satu proses API untuk antrean lokal MVP |
| Tinggi | API expired dan scheduler belum memiliki hubungan jelas | Cek expiry setiap request; sweep target 5 menit |
| Sedang | Tombstone minimal bertentangan dengan kolom non-null | Jelaskan nullable dan CHECK saat terisi |
| Sedang | A/B hanya menyamakan playhead tanpa kompensasi delay model | Wajib verifikasi alignment dan durasi output |
| Sedang | Retry create berpotensi membuat job ganda | Larang retry POST otomatis, tanpa menambah fitur idempotency MVP |
| Sedang | Ukuran file dan total multipart belum dibedakan | Batas stream file dan allowance overhead proxy |

### Verifikasi dan batas hasil
Audit ini adalah review statis dokumen lokal. Tidak ada riset eksternal atau klaim verifikasi lisensi, merek, model, maupun standar. Pemeriksaan tautan lokal, aturan ignore dengan berkas hipotetis, dan git diff --check dipakai untuk memeriksa perubahan. Tidak ada scaffold sehingga tes runtime, lint/typecheck, performa dan keamanan belum dapat dijalankan.

### Skenario wajib setelah GO
Upload invalid/oversize/decode bomb; token hilang/salah; CORS preflight; queue penuh; restart dengan job aktif; DELETE berulang dan DELETE saat inference; expiry saat inference; storage gagal lalu pulih; cleanup output terlambat; alignment A/B serta playback/download berheader token. Ini rencana verifikasi, bukan tes yang sudah lulus.
