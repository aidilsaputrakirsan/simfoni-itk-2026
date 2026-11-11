# SIMFONI ITK 2026 — Slide Workshop (Slidev)

Presentasi Aidil Saputra Kirsan sebagai narasumber workshop **"Integrasi AI untuk Kebijakan dan
Keputusan Strategis yang Berdampak"** di SIMFONI ITK 2026 (LPPM ITK).
Jawab dalam Bahasa Indonesia, santai tapi jelas.

- **Acara:** Selasa, 17 November 2026, 09.30–11.00 WITA, Ruang Rapat 1 LPPM ITK. Moderator: Riki Herliansyah, Ph.D.
- **Format (dari KAK):** paparan 30 menit + diskusi kelompok 60 menit (kelompok campuran pemerintah/industri/ITK).
- **Peserta:** ±70 offline + 80 online — mitra pemerintah & industri, pimpinan unit, dosen/peneliti ITK.
- **Kerangka wajib KAK:** data, model, tata kelola, etika, pengukuran dampak.
- **Luaran wajib KAK:** peta tantangan & peluang AI, rangkuman diskusi + rekomendasi awal, daftar minat kolaborasi (riset/pelatihan/pilot).
- Publik di GitHub Pages: https://myst-tech.com/simfoni-itk-2026/ (repo PUBLIK — lihat "Privasi").

## Benang merah
> AI sudah murah dan mudah diakses. Yang menentukan dampaknya adalah data yang rapi dan aturan
> pemakaian yang jelas — manusia tetap yang memutuskan.

Alur: pertanyaan pembuka → **otak AI** (model = penebak kata; halusinasi; cara membandingkan model) → **3 cara memakai AI** (bikin model sendiri / pasang open-source / API
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
| `slides.md` | 21 slide (2 = tentang pembicara; 4–5 = "Otak AI": penebak kata & halusinasi); frontmatter `bagian:` per slide = teks footer; catatan pembicara di `<!-- -->` |
| `styles/index.css` | seluruh tampilan (token warna di `:root`, kelas `.baris`, `.kolom`, `.alur`, `.sorot`, `.sumber`, `.malam`, `.sampul`) |
| `global-top.vue` | header berjalan (SIMFONI ITK 2026 + bagian, garis tipis) + nomor halaman kanan bawah. HARUS `global-top` |
| `components/HargaTurun.vue` | grafik lereng US$20 → US$0,07 (sumbu log) |
| `components/BiayaLog.vue` | batang log: Rp1,3 T vs Rp190–280 jt/bln vs < Rp150 (muncul per klik) |
| `components/Tangkapan.vue` | rekaman/tangkapan layar: prop `video` (mp4, muted+loop, jalan hanya saat slide aktif, reset saat pindah; `zoom` untuk rekaman bermargin lebar) → cadangan `src` (jpg = frame dari video; juga poster & tampilan ekspor) → bingkai putus-putus |
| `components/TebakKata.vue` | slide 4: pertanyaan lansia → kandidat kata + peluang (ILUSTRASI) → jawaban yakin → "itulah halusinasi"; `clicks: 3` |
| `components/TahuTidakTahu.vue` | slide 5: batang SimpleQA benar/tidak menjawab/salah (o4-mini vs gpt-5-thinking-mini) |
| `components/GerbangTerjawab.vue` | slide 17 "Aturan main…": lima gerbang yang sama, kini dijawab keputusan desain Satu Etam; `clicks: 5` (pengganti tabel) |
| `components/LimaGerbang.vue` | slide 10 lima pertanyaan sebagai 5 gerbang di jalur "rencana pakai AI → keputusan"; klik 1–5 fokus satu pertanyaan + contoh Satu Etam, klik 6 panah "kesalahan paling umum"; `clicks: 6`; ekspor = daftar ringkas |
| `components/AlurData.vue` | slide 11 Satu Etam: label data di RT → **batas privasi** (nama/NIK/kontak/iuran dicoret, tertahan) → jumlah per wilayah → kota (91 indikator/24 OPD) → keputusan; `clicks: 4` |
| `components/Siklus.vue` | slide 16 "Tiga hal…satu siklus": alur Data →(AI)→ Periksa →(keputusan)→ Ukur + panah balik; per klik via frontmatter `clicks: 4` + `$clicks` (pengganti 3 kartu bernomor yang terasa template) |
| `components/Ilustrasi.vue` | ilustrasi line-art: `latih` (chip GPU), `server` (rak + unduh), `api` (aplikasi ⇄ cloud) |
| `global-bottom.vue` | latar hidup: kanvas jaringan titik samar (sebagian mint) + warna latar gelap (karena `.slidev-layout` transparan). Diam di ekspor & reduced-motion |
| `components/Foto.vue` | foto dokumenter berwarna (sedikit diredupkan) + kredit lisensi; zoom pelan saat slide aktif |
| `components/AngkaNaik.vue` | angka menghitung naik saat slide dibuka (280×) |
| `public/foto/` | foto bebas lisensi (Wikimedia/Flickr via Openverse). CC BY/BY-SA WAJIB ada kredit `kredit="Pembuat, Lisensi"` di slide |
| `public/myst-mark.svg`, `public/aidil.png` | logo Myst Tech & foto profil (PNG transparan → dipakai di panel terang `.potret`), dari repo aidilsaputrakirsan.github.io |
| `public/produk/` | cuplikan landing page produk Myst Tech (dari repo aidilsaputrakirsan.github.io) |

Path gambar di prop komponen (`src="/foto/x.jpg"`) diberi `import.meta.env.BASE_URL` di dalam komponen;
`<img>` biasa di slides.md otomatis ikut base. Animasi memakai `useIsSlideActive()` dan selalu tampil
final bila `isPrintMode`.

## Arah desain (penting — user menolak tampilan "AI slop" DAN tampilan kaku/jadul)
Sejak 10 Nov 2026: **gelap elegan** (referensi user: infografis Dicoding — gayanya saja, jangan tiru logo/aset).
Latar hitam pekat `#0b0c0f` (dilukis `global-bottom.vue`), teks `#f4f5f7`, redup `#a0a6b1`, garis `#24272e`,
biru `#4ea1f3` (bagian kunci judul), mint `#5eead4` (nomor 01/02, angka, highlight). Token di `:root` styles/index.css.
Plus Jakarta Sans (judul 800 + teks) + JetBrains Mono (angka, label kecil). Gaya kertas/serif lama DIBUANG.
- Judul = **kalimat pernyataan**, huruf kalimat biasa; bagian kuncinya `<span class="biru">…</span>` (dua warna).
- Hindari grid 3 kartu bernomor (user: "AI banget"); lebih baik diagram alur/siklus yang menunjukkan hubungan antar poin.
- Boleh: kotak berbingkai tipis bersudut bulat (seperlunya), ilustrasi line-art (`Ilustrasi.vue`:
  garis terang + isian mint), nomor mint tebal, foto berwarna asli (sedikit diredupkan) bersudut bulat.
- DILARANG: emoji, gradien, bayangan tebal, blok warna penuh, label kapital di atas setiap judul, ikon tempelan
  yang tidak menjelaskan isi.
- Penekanan: `v-mark` (coretan tangan, warna mint: `v-mark="{ at: N, type: 'underline', color: '#5eead4' }"`) maksimal 1 per slide; `v-click` untuk pengungkapan bertahap.
- Di SVG, ukuran huruf pakai `style="font-size:..px"` (atribut `font-size` tertimpa CSS).
- `.sumber` = catatan sumber di dasar slide (di atas footer); setiap angka luar WAJIB bersumber.
- Cek visual: `npx slidev export --format png --output <folder>` lalu lihat gambarnya; atau Playwright ke dev server.

## Data & sumber (jangan mengarang angka baru)
| Angka | Sumber | Catatan |
|---|---|---|
| Profil pembicara: Dosen SI ITK sejak 2020, Kepala Lab Inovasi Digital FSTI (2024–), Founder PT Myst Tech Core, Ketua RT 44 Sepinggan Baru (2025–), Auditor TI BNSP (2024), Peringkat I Latsar CPNS 2026, 23 publikasi | `~/Projects/aidilsaputrakirsan.github.io/src/data/*` (experience, achievements, publications.openalex.json), poster RT | Perbarui dari repo profil bila berubah |
| GPT-4 ±US$78 jt, Llama 3.1 405B ±US$170 jt, Gemini 1.0 Ultra ±US$191 jt (biaya komputasi latih) | Stanford AI Index 2025 (estimasi bersama Epoch AI), via liputan sekunder | Belum dicek langsung di tabel PDF — user diminta verifikasi |
| SimpleQA: o4-mini benar 24% / salah 75%; gpt-5-thinking-mini benar 22% / salah 26% ("tidak menjawab" = sisanya, ±1% & ±52%) | OpenAI, "Why language models hallucinate" (5 Sep 2025), dari GPT-5 system card | Penyebab halusinasi: evaluasi memberi nilai untuk menebak, bukan "tidak tahu" |
| Harga setara GPT-3.5: US$20 → US$0,07 per 1 jt token (Nov 2022 → Okt 2024), 280× | Stanford AI Index 2025 | Harga untuk kemampuan setara, bukan satu produk |
| Harga setara GPT-4 (MMLU ≥ 86): GPT-4 US$37,50 (Mar 2023) → GPT-4 Turbo US$15 (Nov 2023) → Gemini 1.5 Pro US$2,19 (Mei 2024) → Gemini 2.0 Flash US$0,18 (Feb 2025), ±208× | Epoch AI, “LLM inference prices have fallen rapidly but unequally across tasks” (12 Mar 2025) | Data Epoch berhenti Feb 2025; tidak ada AI Index 2026 yang terverifikasi |
| GuruPintar: 170 permintaan AI, 315.382 token tercatat; temperature koreksi 0,2, pesan siswa 0,6, transkripsi 0,1 | panel admin GuruPintar, 11 Nov 2026 (rekaman) | Agregat. Slide 16 = "pola yang sama di sekolah", bukan jualan |
| Model Satu Etam Nov 2026: DeepSeek V4 Flash US$0,11, Qwen3.5-9B US$0,19, Qwen3-VL-30B US$0,26 per 1 jt token | API publik OpenRouter `/api/v1/models`, 10 Nov 2026 | Blended 3 input : 1 output (sama dgn AI Index/Epoch). Penanda terpisah, BUKAN lanjutan tren. Cek ulang sebelum acara |
| Llama 3.1 405B ±810 GB memori GPU (FP16) → 8–16 GPU H100 | Next Platform (2024), RunPod | Sumber berbeda soal cukup 8 atau perlu 16 |
| H100 US$25–40 rb/unit; sewa US$2–8/GPU/jam | GMI Cloud, Thunder Compute (2025) | Kisaran vendor |
| Rp190–280 jt/bulan | hitungan sendiri: US$2–3 × 8 GPU × 720 jam × Rp16.500 | estimasi |
| Rp1,3 triliun | US$78 jt × Rp16.500 | estimasi |
| Satu Etam: Baca KTP ±Rp5 (rata2 US$0,000295, 5×), Tanya Data ±Rp4 (US$0,000227, 24×), uraian laporan ±Rp5 (US$0,000279, 4×), total 33 pemakaian US$0,008 (< Rp150) | tabel `ai_usages` Satu Etam, 23 Okt – 4 Nov 2026 | uji coba awal; cek ulang sehari sebelum acara |
| 2 RT aktif (RT 44 = 154 rumah, RT 56 = 261 rumah, Kel. Sepinggan Baru) ≈ 415 rumah; 91 indikator / 24 OPD | DB Satu Etam (agregat) | RT lain 0–40 rumah, diduga data uji — konfirmasi ke user |

URL sumber:
- https://openai.com/index/why-language-models-hallucinate/
- https://epoch.ai/data-insights/llm-inference-price-trends
- https://openrouter.ai/api/v1/models
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
- Slide 16 (dulu "Diskusi kelompok") diganti GuruPintar: `public/gurupintar-admin.mp4` (66 dtk, HANYA tab Prompt AI —
  rekaman asli memuat email akun guru asli di tab Penggunaan AI, sudah dipotong dtk 11–77). Diskusi 60 menit (wajib KAK)
  dipandu moderator; info kasus cadangan pindah ke catatan pembicara slide 16.
- Rekaman demo sudah ada: `public/baca-kk.mp4` (39 dtk), `public/tanya-data.mp4` (23 dtk), dikonversi dari .mov dengan
  `avconvert --preset Preset1280x720` (bawaan macOS; tidak ada ffmpeg). Uji putar pakai Playwright `channel: 'chrome'`
  (Chromium bawaan Playwright tidak bisa H.264).
- Kontak di slide penutup masih `[email] · [WhatsApp] · [QR]`.
- Verifikasi angka biaya training di PDF AI Index; konfirmasi jumlah RT/rumah aktif.
- Lembar kerja diskusi (5 pertanyaan + hambatan + minat kolaborasi) + versi Google Form untuk peserta online.
  Draf lengkap naskah, lembar kerja, kasus cadangan, dan Q&A ada di
  `~/Projects/sepingganbaru-rt/materi-simfoni-2026.md` (file lokal, tidak di-commit).
- Opsional: QR ke myst-tech.com, video demo cadangan, ekspor PDF untuk panitia.

## Privasi (repo publik)
Jangan pernah memasukkan data warga asli (nama, NIK, foto KTP/KK, alamat, nomor HP), isi `.env`, atau
dump database ke repo ini. Tangkapan layar hanya dari mode demo (RT `CTH-…`). Angka Satu Etam hanya agregat.
