---
theme: default
title: Integrasi AI untuk Kebijakan dan Keputusan Strategis
info: SIMFONI ITK 2026 — Workshop, Aidil Saputra Kirsan
colorSchema: dark
favicon: /favicon.svg
aspectRatio: 16/9
canvasWidth: 1280
fonts:
  sans: Plus Jakarta Sans
  mono: JetBrains Mono
  weights: '400,500,600,700,800'
  italic: true
transition: fade
drawings:
  persist: false
layout: cover
class: sampul
---

<div>
<p class="mono redup" style="font-size:16px">SIMFONI ITK 2026 — Workshop</p>

# Integrasi AI untuk kebijakan dan <span class="biru">keputusan strategis yang berdampak</span>

<p class="redup" style="font-size:24px;max-width:820px;margin-top:20px">Dari memakai AI, ke mengambil keputusan dengan bantuan AI — yang bisa dipertanggungjawabkan.</p>
</div>

<Foto src="/foto/balikpapan.jpg" :tinggi="150" posisi="center 60%" ket="Balikpapan, Desember 2018" kredit="consigliere ivan, CC0 (Wikimedia Commons)" />

<div class="meta">
<div>
<p><b>Aidil Saputra Kirsan, S.ST., M.Tr.Kom.</b></p>
<p class="redup">Dosen Sistem Informasi ITK · Founder Myst Tech</p>
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

<h1 class="biru" style="margin-top:8px">Sedikit yang memakainya untuk mengambil <span v-mark="{ at: 2, type: 'underline', color: '#5eead4', strokeWidth: 4 }">keputusan</span>.</h1>

</v-click>

<div class="grid gap-12" style="margin-top:72px;grid-template-columns:1fr 1fr 280px;align-items:end">
<div class="kolom">
<p class="no">PERTANYAAN 1</p>
<p>Siapa yang minggu ini memakai ChatGPT, Gemini, Claude, atau Copilot?</p>
</div>
<div class="kolom" v-click>
<p class="no">PERTANYAAN 2</p>
<p>Adakah keputusan di kantor Anda yang diambil dengan bantuan AI — dan bisa dipertanggungjawabkan?</p>
</div>
<Foto src="/foto/angkat-tangan.jpg" :tinggi="210" posisi="center 30%" kredit="USDA, domain publik" />
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

# Ada tiga cara sebuah institusi <span class="biru">memakai AI</span>

</div>

<div class="baris ilus" style="border-top:none;padding:6px 0">
<span class="no"></span><span class="label-kolom">CARA</span><span class="label-kolom">YANG DIBUTUHKAN</span><span></span>
</div>
<div class="baris ilus" v-click>
<span class="no">01</span>
<span class="nama">Membuat model sendiri<br><span class="redup" style="font-size:17px;font-weight:400;letter-spacing:0">seperti ChatGPT, Gemini, Claude</span></span>
<span class="ket">Riset bertahun-tahun, ribuan GPU, ratusan juta dolar</span>
<Ilustrasi jenis="latih" />
</div>
<div class="baris ilus" v-click>
<span class="no">02</span>
<span class="nama">Memasang model open-source<br><span class="redup" style="font-size:17px;font-weight:400;letter-spacing:0">Llama, Qwen, DeepSeek di server sendiri</span></span>
<span class="ket">Server GPU besar dan tim yang merawatnya</span>
<Ilustrasi jenis="server" />
</div>
<div class="baris ilus" v-click>
<span class="no">03</span>
<span class="nama"><span v-mark="{ at: 4, type: 'circle', color: '#5eead4', strokeWidth: 3 }">Memakai API</span>, bayar per pemakaian<br><span class="redup" style="font-size:17px;font-weight:400;letter-spacing:0">model di server penyedia, dihitung per token</span></span>
<span class="ket">Koneksi internet dan aturan data yang ketat</span>
<Ilustrasi jenis="api" />
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

# Melatih satu model besar menelan biaya <span class="biru">ratusan juta dolar</span>

<div class="grid gap-16" style="grid-template-columns: 1.3fr 1fr; margin-top:48px">
<div>

| Model | Biaya komputasi pelatihan |
|---|---|
| GPT-4 | <span class="mono">± US$78 juta</span> |
| Llama 3.1 405B | <span class="mono">± US$170 juta</span> |
| Gemini 1.0 Ultra | <span class="mono">± US$191 juta</span> |

</div>
<div style="padding-top:8px">
<Foto src="/foto/klaster-gpu.jpg" :tinggi="150" posisi="center 40%" ket="Klaster GPU untuk komputasi" kredit="ChrisDag, CC BY 2.0" />
<p class="sorot-kecil" style="margin-top:30px">± Rp1,3 triliun</p>
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

# Model open-source gratis diunduh. <span class="biru">Servernya yang mahal.</span>

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
<Foto src="/foto/ruang-server.jpg" :tinggi="130" posisi="center 45%" kredit="motleypixel, CC BY 2.0" />
<p class="redup" style="font-size:18px;margin-top:14px">Menyewa 8 GPU nonstop</p>
<p class="sorot-kecil">Rp190–280 juta</p>
<p class="redup">setiap bulan</p>
<p style="margin-top:16px;font-size:19px">Kelebihannya: data tidak keluar dari server sendiri. Layak untuk data yang <b>sangat</b> sensitif.</p>
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

# Harga AI <span class="biru">turun ratusan kali</span> sejak 2022

<div class="grid gap-10 items-center" style="grid-template-columns: 700px 1fr; margin-top:18px">
<HargaTurun />
<div>
<p class="redup" style="font-size:15px">Per 1 juta token, untuk kemampuan yang sama</p>
<p class="sorot aksen" style="margin:4px 0 0;font-size:88px"><AngkaNaik :sampai="280" akhiran="×" /></p>
<p class="redup" style="font-size:16px;margin-top:0">setara GPT-3.5, Nov 2022 → Okt 2024</p>
<p class="sorot-kecil biru" style="margin-top:14px">± 200×</p>
<p class="redup" style="font-size:16px;margin-top:0">setara GPT-4, Mar 2023 → Feb 2025</p>
<p style="margin-top:14px;font-size:17px;line-height:1.4">Nov 2026: model yang dipakai Satu Etam <b>US$0,11–0,26</b> per 1 juta token.</p>
<p v-click style="margin-top:8px;font-size:17px;line-height:1.4">Harganya: <b>data kita dikirim ke server pihak lain.</b></p>
</div>
</div>

<p class="sumber">Sumber: Stanford AI Index 2025 (GPT-3.5); Epoch AI, “LLM inference prices have fallen rapidly but unequally across tasks”, Mar 2025 (GPT-4, MMLU); harga OpenRouter 10 Nov 2026 (DeepSeek V4 Flash, Qwen3.5-9B, Qwen3-VL-30B). Harga gabungan 3 input : 1 output.</p>

<!--
Dua garis = dua tingkat kemampuan yang dikunci: setara GPT-3.5 dan setara GPT-4. Harganya turun ratusan kali.
GPT-4: US$37,50 (Mar 2023) → GPT-4 Turbo US$15 → Gemini 1.5 Pro US$2,19 → Gemini 2.0 Flash US$0,18 (Feb 2025), ±208×.
Titik 2026 BUKAN lanjutan garis: itu harga hari ini untuk model yang kami pakai di Satu Etam (DeepSeek V4 Flash, Qwen).
Pesan: harga per token sekarang di kisaran sen dolar — biaya bukan lagi penghalang.
[klik] Jembatan ke tata kelola: murah, tapi data keluar dari institusi kita. Maka harus ada aturan.
-->

---
bagian: Tiga cara memakai AI
---

# Dari triliunan rupiah, <span class="biru">ke ratusan rupiah</span>

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
<h1 style="font-size:64px;margin-top:12px" class="biru">Yang mahal adalah data yang buruk, dan keputusan yang tidak bisa dipertanggungjawabkan.</h1>
</div>

<!--
Jeda. Ini kalimat yang ingin dibawa pulang peserta.
-->

---
bagian: Kerangka
---

<div class="judul-garis">

# Lima pertanyaan sebelum AI dipakai <span class="biru">untuk keputusan</span>

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

# Satu Etam: data dirapikan di RT, <span class="biru">dijumlahkan sampai meja Walikota</span>

<p class="redup" style="margin:10px 0 40px">Sistem Informasi RT Kota Balikpapan — produk Myst Tech, <span class="mono">rt.myst-tech.com</span></p>

<div class="alur" style="margin-top:40px">
<div v-click><p class="tahap">01 · RT</p><p class="judul">Warga dan ketua RT</p><p class="ket">Data rumah, keluarga, dan demografi dicatat rapi di tempat asalnya.</p></div>
<div v-click><p class="tahap">02 · AGREGAT</p><p class="judul">Angka per wilayah</p><p class="ket">Dijumlahkan per RT, kelurahan, kecamatan — tanpa nama, NIK, atau kontak.</p></div>
<div v-click><p class="tahap">03 · KOTA</p><p class="judul">Dashboard Walikota</p><p class="ket">Digabung dengan 91 indikator dari 24 OPD di Portal Satu Data.</p></div>
<div v-click><p class="tahap">04 · KEPUTUSAN</p><p class="judul">Tanya Data</p><p class="ket">Pertanyaan → analisis → saran program, lengkap dengan sumbernya.</p></div>
</div>

<div class="statistik" style="margin-top:48px">
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

# AI yang mengetik. <span class="biru">Ketua RT yang memeriksa.</span>

<div class="grid gap-12" style="grid-template-columns: 1.15fr 1fr; margin-top:32px">
<Tangkapan src="/baca-kk.jpg" video="/baca-kk.mp4" label="Layar tinjau hasil Baca Kartu Keluarga (mode demo)" :tinggi="400" />
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

# AI menerjemahkan pertanyaan. <span class="biru">Angkanya dihitung sistem.</span>

<div class="grid gap-12" style="grid-template-columns: 1fr 1.15fr; margin-top:28px">
<div>
<p class="redup" style="font-size:18px">Walikota mengetik:</p>
<p class="tanya">“Kelurahan mana yang lansianya paling banyak?”</p>

- AI hanya **memilih analisis** yang tepat
- Setiap jawaban menampilkan langkah dan sumber datanya
- Saran program dari **aturan tertulis**, bisa diperiksa Bappeda
- AI tidak tersedia → sistem tetap jalan dengan kata kunci

</div>
<Tangkapan src="/tanya-data.jpg" video="/tanya-data.mp4" label="Tanya Data di dashboard Walikota (mode demo)" :tinggi="420" />
</div>

<!--
Masalah terbesar AI untuk kebijakan: halusinasi — AI bisa mengarang angka dengan sangat meyakinkan.
Solusinya: AI jadi penerjemah pertanyaan, hitungan oleh sistem yang deterministik (input sama → jawaban sama).
-->

---
bagian: Studi kasus — Satu Etam
---

# Biaya AI di Satu Etam: <span class="biru">sekitar lima rupiah per KTP</span>

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

# Aturan main ditulis ke dalam sistem, <span class="biru">bukan di lemari</span>

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

# Tiga hal yang bisa <span class="biru">dimulai besok</span>

<div class="grid grid-cols-3 gap-7" style="margin-top:56px">
<div class="kotak" v-click><p class="no">01</p><h2>Mulai dari data, bukan dari AI</h2><p class="redup">Rapikan data di sumbernya. AI tidak bisa memperbaiki data yang tidak ada.</p></div>
<div class="kotak" v-click><p class="no">02</p><h2>AI membantu, manusia memutuskan</h2><p class="redup">Tentukan di titik mana manusia wajib memeriksa, sebelum sistemnya dibangun.</p></div>
<div class="kotak" v-click><p class="no">03</p><h2>Ukur dengan angka yang bisa dicek</h2><p class="redup">Waktu, biaya, ketepatan sasaran — dan catat setiap pemakaian.</p></div>
</div>

---
bagian: Pola yang sama — GuruPintar
---

# Pola yang sama di sekolah: <span class="biru">aturan AI tertulis, pemakaiannya tercatat</span>

<div class="grid gap-10" style="grid-template-columns: 1.1fr 1fr; margin-top:26px">
<Tangkapan src="/gurupintar-admin.jpg" video="/gurupintar-admin.mp4" label="Panel admin GuruPintar — tab Prompt AI" :tinggi="380" :zoom="1.38" />
<div>

- Tiap fitur AI punya **prompt tertulis**: peran, aturan, format jawaban, bisa dibaca dan diubah admin
- **Model dan temperature dipilih per tugas**: koreksi tugas 0,2 (kaku), draf pesan siswa 0,6
- Setiap permintaan AI **dicatat tokennya** per akun guru
- Nilai akhir tetap **di tangan guru**: hasil AI ditinjau dan bisa diedit

<div class="statistik" style="grid-template-columns:1fr 1fr;gap:24px;margin-top:22px">
<div><p class="sorot-kecil">170</p><p class="redup" style="font-size:16px">permintaan AI tercatat</p></div>
<div><p class="sorot-kecil">315.382</p><p class="redup" style="font-size:16px">token, terpisah teks dan gambar</p></div>
</div>

</div>
</div>

<p class="sumber">Sumber: panel admin GuruPintar (asisten guru, produk Myst Tech), 11 Nov 2026 — angka agregat, tanpa data guru atau siswa.</p>

<!--
Bukan untuk jualan: ini bukti bahwa pola tata kelola Satu Etam bisa ditiru di sektor lain.
Kaitkan ke lima pertanyaan: 02 Peran AI (menilai dengan rubrik guru), 03 Tata kelola (prompt tertulis & bisa diaudit),
05 Dampak (pemakaian dan token tercatat).
Temperature = seberapa "kreatif" jawaban AI: 0 kaku/konsisten, 1 bebas. Untuk menilai dipakai rendah (0,2).
Diskusi kelompok 60 menit dipandu moderator — lembar kerja memakai lima pertanyaan di slide 9.
Kasus cadangan: prioritas bantuan lansia/stunting per kelurahan · prioritas perbaikan jalan · seleksi UMKM mitra binaan.
-->

---
bagian: Penutup
---

# Mari mulai dari satu kelurahan, <span class="biru">satu OPD, satu keputusan</span>

<div class="grid gap-16" style="grid-template-columns: 1fr 1fr; margin-top:48px">
<div class="kolom">
<p class="no">PELUANG KOLABORASI</p>

- **Pilot project** di kelurahan atau OPD
- **Pelatihan** tata kelola AI untuk ASN dan staf
- **Riset** model lokal untuk data sensitif

<Foto src="/foto/kelurahan-manggar.jpg" :tinggi="150" posisi="center 55%" :atas="20" ket="Kantor Kelurahan Manggar, Balikpapan Timur" kredit="Ezagren, CC BY-SA 4.0" />

</div>
<div class="kolom">
<p class="no">MYST TECH · myst-tech.com</p>
<div style="margin-top:10px">
<div class="produk"><img src="/produk/gurupintar.jpg" alt=""><div><p class="nama">GuruPintar</p><p class="ket">asisten guru</p></div></div>
<div class="produk"><img src="/produk/asdospintar.jpg" alt=""><div><p class="nama">AsdosPintar</p><p class="ket">asisten kelas dosen</p></div></div>
<div class="produk"><img src="/produk/skripsipintar.jpg" alt=""><div><p class="nama">SkripsiPintar</p><p class="ket">pendamping skripsi</p></div></div>
<div class="produk"><img src="/produk/manajemen-rt.jpg" alt=""><div><p class="nama">Satu Etam</p><p class="ket">manajemen RT dan dashboard pemkot</p></div></div>
</div>
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
- Epoch AI (Mar 2025), “LLM inference prices have fallen rapidly but unequally across tasks”
- OpenRouter, daftar harga model per 10 Nov 2026
- Next Platform (2024), kebutuhan GPU Llama 3.1 405B; RunPod
- GMI Cloud; Thunder Compute — harga beli dan sewa GPU H100 (2025)
- Catatan pemakaian sistem Satu Etam, tabel ai_usages (agregat, tanpa data pribadi)
- Foto: Wikimedia Commons dan Flickr — CC0, domain publik, CC BY 2.0, CC BY-SA 4.0; kredit tertera di tiap slide

</div>

<p class="sumber">Biaya pelatihan = estimasi AI Index/Epoch AI, bukan rilis resmi perusahaan. Harga GPU = kisaran dari vendor.</p>
