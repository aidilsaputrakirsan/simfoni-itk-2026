---
theme: default
title: Integrasi AI untuk Kebijakan dan Keputusan Strategis
info: SIMFONI ITK 2026 — Workshop, Aidil Saputra Kirsan
colorSchema: light
aspectRatio: 16/9
canvasWidth: 1280
fonts:
  sans: IBM Plex Sans
  serif: Newsreader
  mono: IBM Plex Mono
  weights: '400,500,600'
  italic: true
transition: fade
drawings:
  persist: false
layout: cover
class: sampul
---

<div>
<p class="mono redup" style="font-size:16px">SIMFONI ITK 2026 — Workshop</p>

# Integrasi AI untuk kebijakan dan keputusan strategis yang berdampak

<p class="redup" style="font-size:24px;max-width:820px;margin-top:20px">Dari memakai AI, ke mengambil keputusan dengan bantuan AI — yang bisa dipertanggungjawabkan.</p>
</div>

<div class="meta">
<div>
<p><b>Aidil Saputra Kirsan, S.ST., M.Tr.Kom.</b></p>
<p class="redup">Dosen Sistem Informasi ITK · Founder Myst Tech</p>
</div>
<div>
<p>Selasa, 17 November 2026</p>
<p class="redup">Ruang Rapat 1 LPPM ITK · Moderator: Riki Herliansyah, Ph.D</p>
</div>
</div>

<!--
Perkenalan singkat: dosen SI ITK, pendiri Myst Tech yang membangun produk AI untuk guru, dosen, mahasiswa, dan RT.
Format: 30 menit saya bicara, 60 menit Bapak/Ibu yang bekerja.
-->

---
bagian: Pembuka
---

# Hampir semua dari kita sudah memakai AI.

<v-click>

<h1 class="redup" style="margin-top:8px">Sedikit yang memakainya untuk mengambil <span v-mark.underline.red="2">keputusan</span>.</h1>

</v-click>

<div class="grid grid-cols-2 gap-16" style="margin-top:96px;max-width:980px">
<div class="kolom">
<p class="no">PERTANYAAN 1</p>
<p>Siapa yang minggu ini memakai ChatGPT, Gemini, Claude, atau Copilot?</p>
</div>
<div class="kolom" v-click>
<p class="no">PERTANYAAN 2</p>
<p>Adakah keputusan di kantor Anda yang diambil dengan bantuan AI — dan bisa dipertanggungjawabkan?</p>
</div>
</div>

<!--
[klik] Minta angkat tangan untuk pertanyaan 1 (online: chat/polling). Hampir semua angkat tangan.
[klik] Tunjukkan kalimat kedua.
[klik] Pertanyaan 2: sedikit yang angkat tangan. Itulah jarak yang dibahas hari ini.
-->

---
bagian: Tiga cara memakai AI
---

<div class="judul-garis">

# Ada tiga cara sebuah institusi memakai AI

</div>

<div class="baris" style="border-top:none">
<span class="no"></span><span class="redup" style="font-size:16px">CARA</span><span class="redup" style="font-size:16px">YANG DIBUTUHKAN</span>
</div>
<div class="baris" v-click>
<span class="no">01</span>
<span class="nama">Membuat model sendiri<br><span class="redup" style="font-size:18px;font-family:'IBM Plex Sans'">seperti ChatGPT, Gemini, Claude</span></span>
<span class="ket">Riset bertahun-tahun, ribuan GPU, ratusan juta dolar</span>
</div>
<div class="baris" v-click>
<span class="no">02</span>
<span class="nama">Memasang model open-source<br><span class="redup" style="font-size:18px;font-family:'IBM Plex Sans'">Llama, Qwen, DeepSeek di server sendiri</span></span>
<span class="ket">Server GPU besar dan tim yang merawatnya</span>
</div>
<div class="baris" v-click>
<span class="no aksen">03</span>
<span class="nama"><span v-mark.circle.red="4">Memakai API</span>, bayar per pemakaian<br><span class="redup" style="font-size:18px;font-family:'IBM Plex Sans'">model di server penyedia, dihitung per token</span></span>
<span class="ket">Koneksi internet dan aturan data yang ketat</span>
</div>

<!--
Institusi kita (pemda, perusahaan daerah, kampus) realistisnya di cara 3, kadang 2.
Model = "otak" AI hasil pelatihan. Open-source/open-weight = file model boleh diunduh dan dijalankan sendiri.
API = model di server penyedia; aplikasi mengirim pertanyaan lewat internet.
Token = potongan kata untuk tagihan (±¾ kata Inggris). Harga ditulis per 1 juta token.
-->

---
bagian: Tiga cara memakai AI
---

# Melatih satu model besar menelan biaya ratusan juta dolar

<div class="grid gap-16" style="grid-template-columns: 1.3fr 1fr; margin-top:48px">
<div>

| Model | Biaya komputasi pelatihan |
|---|---|
| GPT-4 | <span class="mono">± US$78 juta</span> |
| Llama 3.1 405B | <span class="mono">± US$170 juta</span> |
| Gemini 1.0 Ultra | <span class="mono">± US$191 juta</span> |

</div>
<div style="padding-top:8px">
<p class="sorot-kecil">± Rp1,3 triliun</p>
<p class="redup" style="margin-top:12px">untuk <i>sekali</i> melatih GPT-4 — belum termasuk gaji peneliti dan riset bertahun-tahun sebelumnya.</p>
</div>
</div>

<p class="sumber">Sumber: Stanford AI Index 2025, estimasi bersama Epoch AI — bukan angka resmi perusahaan. Kurs ±Rp16.500/US$.</p>

<!--
Arsitektur dasar AI modern (Transformer) terbit 2017; ChatGPT muncul akhir 2022.
Ini permainan segelintir perusahaan raksasa. Bagi kita: tidak perlu, dan tidak masuk akal.
-->

---
bagian: Tiga cara memakai AI
---

# Model open-source gratis diunduh. Servernya yang mahal.

<div class="grid gap-16" style="grid-template-columns: 1.2fr 1fr; margin-top:48px">
<div>

| Kebutuhan | Kisaran |
|---|---|
| Memori GPU untuk Llama 3.1 405B | <span class="mono">± 810 GB</span> |
| Jumlah GPU kelas H100 | <span class="mono">8–16 unit</span> |
| Harga satu GPU H100 | <span class="mono">US$25–40 ribu</span> |
| Sewa cloud, per GPU per jam | <span class="mono">US$2–8</span> |

</div>
<div style="padding-top:8px">
<p class="redup" style="font-size:18px">Menyewa 8 GPU nonstop</p>
<p class="sorot-kecil">Rp190–280 juta</p>
<p class="redup">setiap bulan</p>
<p style="margin-top:28px;font-size:19px">Kelebihannya: data tidak keluar dari server sendiri. Layak untuk data yang <b>sangat</b> sensitif.</p>
</div>
</div>

<p class="sumber">Sumber: Next Platform (2024); survei harga vendor cloud 2025 — kisaran indikatif. Estimasi sewa: US$2–3 × 8 GPU × 720 jam.</p>

<!--
Kekurangan: mahal, butuh tim GPU, model cepat ketinggalan.
Model kecil (7–30 miliar parameter) bisa jalan di 1 GPU: peluang riset kolaborasi ITK untuk data sensitif.
Sumber berbeda pendapat apakah 8 H100 cukup untuk versi penuh, makanya "8–16".
-->

---
bagian: Tiga cara memakai AI
---

# Harga memakai AI turun 280 kali dalam dua tahun

<div class="grid gap-12 items-center" style="grid-template-columns: 640px 1fr; margin-top:28px">
<HargaTurun />
<div>
<p class="redup" style="font-size:18px">Per 1 juta token, untuk kemampuan setara GPT-3.5</p>
<p class="sorot aksen" style="margin-top:32px">280×</p>
<p style="margin-top:20px">Inilah yang membuat pengembang kecil di Balikpapan bisa membangun produk AI.</p>
<p v-click style="margin-top:16px">Harganya: <b>data kita dikirim ke server pihak lain.</b></p>
</div>
</div>

<p class="sumber">Sumber: Stanford AI Index 2025 — membandingkan harga untuk kemampuan setara, bukan harga satu produk yang sama.</p>

<!--
[klik] Jembatan ke tata kelola: murah, tapi data keluar dari institusi kita. Maka harus ada aturan.
-->

---
bagian: Tiga cara memakai AI
---

# Dari triliunan rupiah, ke ratusan rupiah

<p class="redup" style="margin:8px 0 36px">Biaya tiap cara, dalam rupiah.</p>

<BiayaLog />

<p class="sumber">Estimasi dari slide sebelumnya; baris terakhir dari catatan pemakaian sistem Satu Etam (tabel ai_usages), 23 Okt – 4 Nov 2026.</p>

<!--
[klik] Cara 1: triliun. [klik] Cara 2: ratusan juta per bulan. [klik] Cara 3: ratusan rupiah.
Skala logaritmik: kalau digambar biasa, batang ketiga tidak akan terlihat sama sekali.
-->

---
layout: center
class: malam
bagian: Tiga cara memakai AI
---

<div style="max-width:1000px">
<h1 style="font-size:64px">AI sudah murah.</h1>
<h1 style="font-size:64px;margin-top:12px" class="redup">Yang mahal adalah data yang buruk, dan keputusan yang tidak bisa dipertanggungjawabkan.</h1>
</div>

<!--
Jeda. Ini kalimat yang ingin dibawa pulang peserta.
-->

---
bagian: Kerangka
---

<div class="judul-garis">

# Lima pertanyaan sebelum AI dipakai untuk keputusan

</div>

<div class="baris" v-click><span class="no">01</span><span class="nama">Data</span><span class="ket">Datanya ada dan rapi? Siapa pemiliknya? Terbaru tahun berapa?</span></div>
<div class="baris" v-click><span class="no">02</span><span class="nama">Peran AI</span><span class="ket">Membaca, merangkum, menghitung, atau menyarankan?</span></div>
<div class="baris" v-click><span class="no">03</span><span class="nama">Tata kelola</span><span class="ket">Siapa yang memutuskan, siapa yang memeriksa, adakah jejak audit?</span></div>
<div class="baris" v-click><span class="no">04</span><span class="nama">Etika & privasi</span><span class="ket">Data pribadi apa yang ikut terkirim? Sesuai UU PDP? Siapa yang bisa dirugikan?</span></div>
<div class="baris" v-click><span class="no">05</span><span class="nama">Dampak</span><span class="ket">Diukur dengan angka apa: waktu, biaya, ketepatan sasaran?</span></div>

<!--
Lima pertanyaan ini dipakai lagi di lembar kerja diskusi.
Kesalahan paling umum: langsung lompat ke nomor 2 (memilih AI) sebelum nomor 1 (data) beres.
-->

---
bagian: Studi kasus — Satu Etam
---

# Satu Etam: data dirapikan di RT, dijumlahkan sampai meja Walikota

<p class="redup" style="margin:10px 0 40px">Sistem Informasi RT Kota Balikpapan — produk Myst Tech, <span class="mono">rt.myst-tech.com</span></p>

<div class="alur" style="margin-top:72px">
<div v-click><p class="tahap">01 · RT</p><p class="judul">Warga dan ketua RT</p><p class="ket">Data rumah, keluarga, dan demografi dicatat rapi di tempat asalnya.</p></div>
<div v-click><p class="tahap">02 · AGREGAT</p><p class="judul">Angka per wilayah</p><p class="ket">Dijumlahkan per RT, kelurahan, kecamatan — tanpa nama, NIK, atau kontak.</p></div>
<div v-click><p class="tahap">03 · KOTA</p><p class="judul">Dashboard Walikota</p><p class="ket">Digabung dengan 91 indikator dari 24 OPD di Portal Satu Data.</p></div>
<div v-click><p class="tahap">04 · KEPUTUSAN</p><p class="judul">Tanya Data</p><p class="ket">Pertanyaan → analisis → saran program, lengkap dengan sumbernya.</p></div>
</div>

<div class="grid grid-cols-3 gap-12" style="margin-top:64px;border-top:1px solid #cfc8b8;padding-top:18px">
<div><p class="sorot-kecil">2 RT</p><p class="redup">sudah berjalan: RT 44 & RT 56, Kel. Sepinggan Baru</p></div>
<div><p class="sorot-kecil">± 415</p><p class="redup">rumah tercatat</p></div>
<div><p class="sorot-kecil">91</p><p class="redup">indikator dari 24 OPD di Ruang Dinas Walikota</p></div>
</div>

<!--
Keputusan kota yang baik butuh data dari bawah. Selama ini data RT ada di buku tulis dan Excel yang berbeda-beda.
Satu Etam merapikan dari bawah, lalu menjumlahkan ke atas tanpa membawa data pribadi.
-->

---
bagian: Studi kasus — Satu Etam
---

# AI yang mengetik. Ketua RT yang memeriksa.

<div class="grid gap-12" style="grid-template-columns: 1.15fr 1fr; margin-top:32px">
<Tangkapan src="/baca-kk.png" label="Layar tinjau hasil Baca Kartu Keluarga (mode demo)" :tinggi="400" />
<div>

- Ketua RT memfoto KTP atau Kartu Keluarga, formulir terisi sendiri
- Sistem memeriksa: NIK 16 digit, tanggal lahir dan jenis kelamin dicocokkan dengan kode NIK
- Hasil **tidak langsung disimpan** — ditinjau dulu, isian dari AI diberi tanda warna
- Foto tidak disimpan, jawaban AI tidak dicatat

<p class="redup" style="margin-top:24px;font-size:18px">Prinsip <i>human-in-the-loop</i>: manusia tetap di dalam alur.</p>
</div>
</div>

<!--
DEMO ±3 menit: pakai foto KTP CONTOH (mode demo), bukan KTP warga asli.
Di kode: PembacaKtp / PembacaKk + layar tinjau TinjauKkDialog. Model Qwen3-VL lewat OpenRouter, dengan model cadangan.
-->

---
bagian: Studi kasus — Satu Etam
---

# AI menerjemahkan pertanyaan. Angkanya dihitung sistem.

<div class="grid gap-12" style="grid-template-columns: 1fr 1.15fr; margin-top:28px">
<div>
<p class="redup" style="font-size:18px">Walikota mengetik:</p>
<p class="tanya">“Kelurahan mana yang lansianya paling banyak?”</p>

- AI hanya **memilih analisis** yang tepat
- Setiap jawaban menampilkan langkah dan sumber datanya
- Saran program dari **aturan tertulis**, bisa diperiksa Bappeda
- AI tidak tersedia → sistem tetap jalan dengan kata kunci

</div>
<Tangkapan src="/tanya-data.png" label="Tanya Data di dashboard Walikota (mode demo)" :tinggi="420" />
</div>

<!--
Masalah terbesar AI untuk kebijakan: halusinasi — AI bisa mengarang angka dengan sangat meyakinkan.
Solusinya: AI jadi penerjemah pertanyaan, hitungan oleh sistem yang deterministik (input sama → jawaban sama).
-->

---
bagian: Studi kasus — Satu Etam
---

# Biaya AI di Satu Etam: sekitar lima rupiah per KTP

<div class="grid gap-16" style="grid-template-columns: 1.3fr 1fr; margin-top:44px">
<div>

| Fitur | Pemakaian | <span class="angka">Rata-rata</span> |
|---|---|---|
| Baca KTP | <span class="mono">5×</span> | <span class="mono">± Rp5</span> |
| Tanya Data (Walikota) | <span class="mono">24×</span> | <span class="mono">± Rp4</span> |
| Bantu tulis laporan RT | <span class="mono">4×</span> | <span class="mono">± Rp5</span> |
| **Total** | <span class="mono">33×</span> | <span class="mono"><b>&lt; Rp150</b></span> |

</div>
<div style="padding-top:8px">
<p>Setiap pemakaian tercatat: fitur, model, jumlah token, biaya.</p>
<p style="margin-top:20px" class="redup">Biaya bukan lagi alasan untuk tidak mulai — yang mahal adalah merapikan data dan melatih orang.</p>
</div>
</div>

<p class="sumber">Sumber: catatan pemakaian sistem Satu Etam (tabel ai_usages), 23 Okt – 4 Nov 2026, uji coba awal. Kurs ±Rp16.500/US$.</p>

<!--
Angka mentah: scan_ktp rata-rata US$0,000295; tanya_data US$0,000227; uraian_kegiatan US$0,000279; total US$0,008.
Sampel kecil — sebut "uji coba awal". Cek ulang angkanya sehari sebelum acara.
-->

---
bagian: Studi kasus — Satu Etam
---

# Aturan main ditulis ke dalam sistem, bukan di lemari

<div style="margin-top:36px">

| Keputusan desain | Menjawab pertanyaan |
|---|---|
| AI membaca, manusia memeriksa dan menyimpan | 03 · Tata kelola |
| Angka dihitung sistem, sumber selalu ditampilkan | 02 · Peran AI |
| Ke AI hanya angka agregat — tanpa nama, NIK, kontak, iuran | 04 · Etika & privasi |
| Penyedia AI wajib *zero data retention*, tanpa itu permintaan ditolak | 04 · Etika & privasi |
| Data dinas yang lebih dari dua tahun diberi tanda “data lama” | 01 · Data |
| Setiap pemakaian AI tercatat lengkap dengan biayanya | 05 · Dampak |

</div>

<!--
Tata kelola bukan dokumen di lemari — ia ditulis ke dalam sistem. Pemerintah dan industri bisa meniru caranya, apa pun aplikasinya.
ZDR = penyedia AI tidak menyimpan isi permintaan dan tidak memakainya untuk melatih model.
-->

---
bagian: Pelajaran
---

# Tiga hal yang bisa dimulai besok

<div class="grid grid-cols-3 gap-12" style="margin-top:64px">
<div class="kolom" v-click><p class="no">01</p><h2>Mulai dari data, bukan dari AI</h2><p class="redup">Rapikan data di sumbernya. AI tidak bisa memperbaiki data yang tidak ada.</p></div>
<div class="kolom" v-click><p class="no">02</p><h2>AI membantu, manusia memutuskan</h2><p class="redup">Tentukan di titik mana manusia wajib memeriksa, sebelum sistemnya dibangun.</p></div>
<div class="kolom" v-click><p class="no">03</p><h2>Ukur dengan angka yang bisa dicek</h2><p class="redup">Waktu, biaya, ketepatan sasaran — dan catat setiap pemakaian.</p></div>
</div>

---
bagian: Diskusi kelompok
---

# Giliran Bapak dan Ibu

<div class="grid gap-16" style="grid-template-columns: 1fr 1fr; margin-top:44px">
<div>

- Kelompok campuran: pemerintah, industri, ITK
- Pilih **satu keputusan nyata** di institusi Anda
- Jawab lima pertanyaan di lembar kerja
- Presentasi kilat tiga menit per kelompok

</div>
<div>

| Menit | Kegiatan |
|---|---|
| <span class="mono">00–05</span> | Pembagian kelompok |
| <span class="mono">05–35</span> | Kelompok bekerja |
| <span class="mono">35–55</span> | Presentasi kilat |
| <span class="mono">55–60</span> | Rangkuman |

</div>
</div>

<p class="sumber">Kasus cadangan: prioritas bantuan lansia/stunting per kelurahan · prioritas perbaikan jalan · seleksi UMKM mitra binaan.</p>

<!--
Peserta online: breakout room / Google Form. Narasumber dan moderator berkeliling.
Hasil lembar kerja = peta tantangan & peluang, rekomendasi awal, daftar minat kolaborasi (luaran KAK).
-->

---
bagian: Penutup
---

# Mari mulai dari satu kelurahan, satu OPD, satu keputusan

<div class="grid gap-16" style="grid-template-columns: 1fr 1fr; margin-top:48px">
<div class="kolom">
<p class="no">PELUANG KOLABORASI</p>

- **Pilot project** di kelurahan atau OPD
- **Pelatihan** tata kelola AI untuk ASN dan staf
- **Riset** model lokal untuk data sensitif

</div>
<div class="kolom">
<p class="no">MYST TECH · myst-tech.com</p>

- GuruPintar — asisten guru
- AsdosPintar — asisten kelas dosen
- SkripsiPintar — pendamping skripsi
- Satu Etam — manajemen RT dan dashboard pemkot

</div>
</div>

<p class="sumber">Kontak: [email] · [WhatsApp] · [QR]</p>

<!--
Satu slide saja, jangan berubah jadi sesi jualan. Kaitkan dengan Pusat Riset TIK Smart City ITK di sesi siang.
-->

---
bagian: Referensi
---

# Sumber

<div style="margin-top:32px;font-size:19px">

- Stanford HAI, *AI Index Report 2025*
- Liputan AI Index 2025: Tom’s Hardware; WisdomTree, “280x cheaper”
- Next Platform (2024), kebutuhan GPU Llama 3.1 405B; RunPod
- GMI Cloud; Thunder Compute — harga beli dan sewa GPU H100 (2025)
- Catatan pemakaian sistem Satu Etam, tabel ai_usages (agregat, tanpa data pribadi)

</div>

<p class="sumber">Biaya pelatihan = estimasi AI Index/Epoch AI, bukan rilis resmi perusahaan. Harga GPU = kisaran dari vendor.</p>
