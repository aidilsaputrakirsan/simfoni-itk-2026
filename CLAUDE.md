# SIMFONI ITK 2026 — Slide Workshop (Slidev)

Presentasi Aidil Saputra Kirsan sebagai narasumber workshop **"Integrasi AI untuk Kebijakan dan
Keputusan Strategis yang Berdampak"** di SIMFONI ITK 2026 (LPPM ITK).
Jawab dalam Bahasa Indonesia, santai tapi jelas.

- **Acara:** Selasa, 17 November 2026, 09.30–11.00 WITA, Ruang Rapat 1 LPPM ITK. Moderator: Riki Herliansyah, Ph.D.
- **Format (dari KAK):** paparan 30 menit + diskusi kelompok 60 menit (kelompok campuran pemerintah/industri/ITK).
- **Peserta:** ±70 offline + 80 online — mitra pemerintah & industri, pimpinan unit, dosen/peneliti ITK.
- **Kerangka wajib KAK:** data, model, tata kelola, etika, pengukuran dampak.
- **Luaran wajib KAK:** peta tantangan & peluang AI, rangkuman diskusi + rekomendasi awal, daftar minat kolaborasi (riset/pelatihan/pilot).
- Publik di GitHub Pages: https://aidilsaputrakirsan.github.io/simfoni-itk-2026/ (repo PUBLIK — lihat "Privasi").

## Benang merah
> AI sudah murah dan mudah diakses. Yang menentukan dampaknya adalah data yang rapi dan aturan
> pemakaian yang jelas — manusia tetap yang memutuskan.

Alur: pertanyaan pembuka → **3 cara memakai AI** (bikin model sendiri / pasang open-source / API
bayar per token) beserta biayanya → pernyataan inti → **5 pertanyaan kerangka** → **studi kasus
Satu Etam** (produk Myst Tech: sistem RT Balikpapan → dashboard Walikota) → 3 pelajaran → diskusi → penutup.
Studi kasus = bukti benang merah, BUKAN sesi jualan (produk Myst Tech lain cukup 1 slide penutup).

## Jalankan
```bash
npm install
npm run dev            # http://localhost:3030  · presenter: /presenter
npm run build          # ke dist/
npm run export         # PDF (playwright-chromium sudah jadi devDependency)
```
Node 22 lewat mise (`.nvmrc`). Slidev v53.1.0 (butuh Node ≥ 22.12).
Deploy: push ke `main` → GitHub Actions (`.github/workflows/deploy.yml`) build dengan
`--base /simfoni-itk-2026/` → GitHub Pages. User commit & push sendiri (GitHub Desktop) kecuali minta.
Commit atas nama user, TANPA `Co-Authored-By: Claude` / atribusi Claude.

## Struktur
| File | Isi |
|---|---|
| `slides.md` | 18 slide; frontmatter `bagian:` per slide = teks footer; catatan pembicara di `<!-- -->` |
| `styles/index.css` | seluruh tampilan (token warna di `:root`, kelas `.baris`, `.kolom`, `.alur`, `.sorot`, `.sumber`, `.malam`, `.sampul`) |
| `global-top.vue` | footer berjalan (bagian + nomor halaman). HARUS `global-top`: `global-bottom` tertutup latar slide yang opak |
| `components/HargaTurun.vue` | grafik lereng US$20 → US$0,07 (sumbu log) |
| `components/BiayaLog.vue` | batang log: Rp1,3 T vs Rp190–280 jt/bln vs < Rp150 (muncul per klik) |
| `components/Tangkapan.vue` | bingkai tangkapan layar; file belum ada → bingkai putus-putus berisi petunjuk |

## Arah desain (penting — user menolak tampilan "AI slop")
Gaya **laporan kebijakan editorial**: kertas `#f4f1ea`, tinta `#1c1b19`, satu aksen merah bata `#a8361b`
(hemat), slide gelap `#1d2230` hanya untuk pernyataan inti. Newsreader (judul, serif) + IBM Plex Sans (teks)
+ IBM Plex Mono (angka, label kecil, footer).
- Judul = **kalimat pernyataan** (assertion), bukan topik. Huruf kalimat biasa, bukan Title Case.
- DILARANG: label kapital di atas setiap judul, kartu berbingkai/bayangan, nomor dalam kotak/lingkaran,
  blok warna penuh, gradien, emoji, ikon dekoratif, grid 3 kartu seragam.
- Pakai: garis tipis (hairline), baris ala tabel laporan, angka monospace rata kanan, banyak ruang kosong,
  grafik sungguhan, tangkapan layar aplikasi asli.
- Penekanan: `v-mark` (coretan tangan) maksimal 1 per slide; `v-click` untuk pengungkapan bertahap.
- Di SVG, ukuran huruf pakai `style="font-size:..px"` (atribut `font-size` tertimpa CSS).
- `.sumber` = catatan sumber di dasar slide (di atas footer); setiap angka luar WAJIB bersumber.
- Cek visual: `npx slidev export --format png --output <folder>` lalu lihat gambarnya; atau Playwright ke dev server.

## Data & sumber (jangan mengarang angka baru)
| Angka | Sumber | Catatan |
|---|---|---|
| GPT-4 ±US$78 jt, Llama 3.1 405B ±US$170 jt, Gemini 1.0 Ultra ±US$191 jt (biaya komputasi latih) | Stanford AI Index 2025 (estimasi bersama Epoch AI), via liputan sekunder | Belum dicek langsung di tabel PDF — user diminta verifikasi |
| Harga setara GPT-3.5: US$20 → US$0,07 per 1 jt token (Nov 2022 → Okt 2024), 280× | Stanford AI Index 2025 | Harga untuk kemampuan setara, bukan satu produk |
| Llama 3.1 405B ±810 GB memori GPU (FP16) → 8–16 GPU H100 | Next Platform (2024), RunPod | Sumber berbeda soal cukup 8 atau perlu 16 |
| H100 US$25–40 rb/unit; sewa US$2–8/GPU/jam | GMI Cloud, Thunder Compute (2025) | Kisaran vendor |
| Rp190–280 jt/bulan | hitungan sendiri: US$2–3 × 8 GPU × 720 jam × Rp16.500 | estimasi |
| Rp1,3 triliun | US$78 jt × Rp16.500 | estimasi |
| Satu Etam: Baca KTP ±Rp5 (rata2 US$0,000295, 5×), Tanya Data ±Rp4 (US$0,000227, 24×), uraian laporan ±Rp5 (US$0,000279, 4×), total 33 pemakaian US$0,008 (< Rp150) | tabel `ai_usages` Satu Etam, 23 Okt – 4 Nov 2026 | uji coba awal; cek ulang sehari sebelum acara |
| 2 RT aktif (RT 44 = 154 rumah, RT 56 = 261 rumah, Kel. Sepinggan Baru) ≈ 415 rumah; 91 indikator / 24 OPD | DB Satu Etam (agregat) | RT lain 0–40 rumah, diduga data uji — konfirmasi ke user |

URL sumber:
- https://hai-production.s3.amazonaws.com/files/hai_ai-index-report-2025_chapter1_final.pdf
- https://www.tomshardware.com/tech-industry/artificial-intelligence/ai-costs-drop-280-fold-but-harmful-incidents-rise-56-percent-in-last-year-stanford-2025-ai-report-highlights-china-us-competition
- https://www.nextplatform.com/ai/2024/07/29/stacking-up-amd-versus-nvidia-for-llama-31-gpu-inference/1656756
- https://www.gmicloud.ai/blog/nvidia-h100-gpu-pricing-2025-rent-vs-buy-cost-analysis
- https://www.thundercompute.com/blog/nvidia-h100-pricing

## Fakta Satu Etam yang dipakai (dari codebase ~/Projects/sepingganbaru-rt)
- Baca KTP/KK (`PembacaKtp`/`PembacaKk`, model Qwen3-VL via OpenRouter + cadangan): hasil ditinjau ketua RT
  dulu (`TinjauKkDialog`), isian AI bertanda warna, foto tidak disimpan, jawaban AI tidak di-log, NIK dicek
  (16 digit, tgl lahir/jenis kelamin vs kode NIK).
- Tanya Data (Walikota): AI hanya memilih kelas analisis (tool), angka dihitung sistem, sumber selalu tampil,
  saran program dari aturan tertulis (`config/program_bantuan.php`), fallback pencocok kata kunci bila AI mati.
- Privasi: ke AI hanya angka agregat (tanpa nama/NIK/kontak/iuran); OpenRouter dipaksa ZDR
  (`data_collection: deny, zdr: true`); setiap pemakaian dicatat di `ai_usages`.
- Ruang Dinas: 24 OPD, 91 indikator Portal Satu Data; data > 2 tahun ditandai "data lama".

## Belum selesai (TODO)
- Tangkapan layar asli (MODE DEMO, bukan data warga): `public/baca-kk.png`, `public/tanya-data.png`.
- Kontak di slide penutup masih `[email] · [WhatsApp] · [QR]`.
- Verifikasi angka biaya training di PDF AI Index; konfirmasi jumlah RT/rumah aktif.
- Lembar kerja diskusi (5 pertanyaan + hambatan + minat kolaborasi) + versi Google Form untuk peserta online.
  Draf lengkap naskah, lembar kerja, kasus cadangan, dan Q&A ada di
  `~/Projects/sepingganbaru-rt/materi-simfoni-2026.md` (file lokal, tidak di-commit).
- Opsional: QR ke myst-tech.com, video demo cadangan, ekspor PDF untuk panitia.

## Privasi (repo publik)
Jangan pernah memasukkan data warga asli (nama, NIK, foto KTP/KK, alamat, nomor HP), isi `.env`, atau
dump database ke repo ini. Tangkapan layar hanya dari mode demo (RT `CTH-…`). Angka Satu Etam hanya agregat.
