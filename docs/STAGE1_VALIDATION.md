# Stage 1 — Strategic validation (draft)

## Domain dan status
AI/ML × speech enhancement. **Verdict: PIVOT TERARAH; GO tertunda.** Ini bukan laporan hasil riset kompetisi.

## Hipotesis produk
- Target awal: mahasiswa dan pembuat konten yang merekam percakapan di lingkungan berisik.
- Pain: ucapan sulit dipahami akibat kebisingan latar.
- Angle: fokus pada intelligibility dan pelestarian karakter suara, bukan klaim menghapus seluruh noise.
- Problem question: Bagaimana membersihkan noise tanpa merusak informasi ucapan?
- Nama kerja: Nirava. Nama ini telah digunakan pihak lain; belum ada pemeriksaan merek, domain, atau ketersediaan repository secara menyeluruh.

## ChatGPT test
Aplikasi memproses audio sungguhan; hasil tidak dapat digantikan dengan satu jawaban teks. Lulus secara konseptual, tetap perlu demo.

## Six winning-pattern checks
1. Failure mode: noise berkurang tetapi konsonan/ucapan ikut rusak — perlu diuji.
2. Stakes: rekaman penting menjadi sulit dipahami; hindari klaim bencana tanpa bukti.
3. Side-by-side: satu layar, audio original vs enhanced, playback tersinkron.
4. Framing: noise reduction vs speech preservation.
5. Judging proof: hasil audio nyata + metrik evaluasi + batasan.
6. Naming: nama harus membantu orang menebak manfaat; lakukan uji pengguna.

## Demo concept
Unggah klip noisy berizin → proses → dengarkan A/B dengan posisi playhead sama → unduh. Wow moment = peningkatan keterdengaran yang bisa diverifikasi, bukan animasi kosmetik.

## Nine-lens provisional scoring (1–10; judgement, bukan data)
Pain 8; differentiation 4; feasibility 7; judge appeal 7; scalability 6; winning chance 5; uniqueness 4; wow 8; ChatGPT test 8.

## Blocking questions sebelum GO
- Nama acara/mata kuliah dan rubrik resmi? Apakah **model generatif** diwajibkan?
- Tema/track, durasi, tenggat, tim, perangkat GPU, anggaran deployment?
- Batasan API/model pretrained dan kebutuhan training/evaluasi?
- Contoh pemenang terdahulu (jika benar-benar hackathon)?
- Apakah audio pengguna boleh diproses di server, dan berapa retensinya?

## Validasi eksternal yang masih harus dikerjakan
Riset 3–5 kompetitor relevan, 2–3 case study pemenang pada domain serupa jika ada kompetisi, tes 3–5 sampel noisy, cek lisensi model, evaluasi keterbacaan nama.

## Gate GO
GO hanya bila rubrik AI cocok, demo terukur realistis, target pengguna jelas, dan biaya komputasi/hosting memadai. Jika wajib generatif, evaluasi model generatif speech restoration sebelum memilih engine.
