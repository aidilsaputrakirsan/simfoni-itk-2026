<script setup>
// Slide "Lima pertanyaan": lima GERBANG yang dilewati sebelum AI dipakai untuk keputusan.
// Per klik (frontmatter slide: `clicks: 6`): klik 1–5 = gerbang ke-n aktif (sebelumnya jadi centang),
// panel fokus menampilkan pertanyaannya + contoh di Satu Etam; klik 6 = panah "kesalahan paling umum"
// (lompat ke Peran AI sebelum Data beres). Mode ekspor: semua gerbang centang + daftar ringkas lima pertanyaan.
// Contoh Satu Etam = fakta di CLAUDE.md.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const cetak = computed(() => isPrintMode.value)
const k = computed(() => (cetak.value ? 99 : $clicks.value))
const aktif = computed(() => (k.value >= 6 ? 6 : k.value)) // 0 = belum ada, 1..5 = gerbang aktif, 6 = semua lewat

const gerbang = [
  { no: '01', nama: 'Data', tanya: 'Datanya ada dan rapi? Siapa pemiliknya? Terbaru tahun berapa?',
    contoh: 'Data rumah dirapikan dulu di RT; data dinas lebih dari dua tahun ditandai “data lama”.' },
  { no: '02', nama: 'Peran AI', tanya: 'Membaca, merangkum, menghitung, atau menyarankan?',
    contoh: 'AI membaca KTP dan memilih jenis analisis — angkanya tetap dihitung sistem.' },
  { no: '03', nama: 'Tata kelola', tanya: 'Siapa yang memutuskan, siapa yang memeriksa, adakah jejak audit?',
    contoh: 'Ketua RT meninjau sebelum menyimpan; setiap pemakaian AI tercatat.' },
  { no: '04', nama: 'Etika & privasi', tanya: 'Data pribadi apa yang ikut terkirim? Sesuai UU PDP? Siapa yang bisa dirugikan?',
    contoh: 'Ke AI hanya angka agregat; penyedia wajib zero data retention.' },
  { no: '05', nama: 'Dampak', tanya: 'Diukur dengan angka apa: waktu, biaya, ketepatan sasaran?',
    contoh: 'Biaya tiap pemakaian tercatat — sekitar lima rupiah per KTP.' },
]

const W = 1120, Y = 64, R = 22
const x0 = 120, x1 = W - 120 // titik awal & akhir jalur
const X = gerbang.map((_, i) => x0 + ((i + 1) * (x1 - x0)) / 6)
const jalurPj = x1 - x0
const majuPj = computed(() => (aktif.value === 0 ? 0 : aktif.value >= 6 ? jalurPj : X[aktif.value - 1] - x0))
const lompat = `M${x0} ${Y - 10} C ${x0 + 30} ${Y - 70}, ${X[1] - 30} ${Y - 70}, ${X[1]} ${Y - R - 6}`
</script>

<template>
  <div class="gerbang" :style="{ width: W + 'px' }">
    <svg :width="W" :height="Y + 58" :viewBox="`0 0 ${W} ${Y + 58}`" fill="none" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <!-- jalur dasar -->
      <line :x1="x0" :x2="x1" :y1="Y" :y2="Y" stroke="#24272e" stroke-width="2" stroke-dasharray="3 7" />
      <!-- jalur yang sudah dilewati -->
      <line :x1="x0" :x2="x1" :y1="Y" :y2="Y" stroke="#5eead4" stroke-width="3" class="maju"
            :style="{ strokeDasharray: jalurPj, strokeDashoffset: jalurPj - majuPj }" />
      <!-- awal & akhir -->
      <circle :cx="x0" :cy="Y" r="6" fill="#a0a6b1" />
      <text :x="x0" :y="Y + 44" text-anchor="middle" fill="#a0a6b1" style="font-size:14px;font-family:'Plus Jakarta Sans'">rencana pakai AI</text>
      <path :d="`M${x1 - 10} ${Y - 9} L${x1} ${Y} L${x1 - 10} ${Y + 9}`" :stroke="k >= 5 ? '#5eead4' : '#343842'" stroke-width="3" />
      <text :x="x1" :y="Y + 44" text-anchor="middle" :fill="k >= 5 ? '#f4f5f7' : '#6b7280'" style="font-size:14px;font-weight:700;font-family:'Plus Jakarta Sans'">keputusan</text>

      <!-- lima gerbang -->
      <g v-for="(g, i) in gerbang" :key="g.no">
        <circle :cx="X[i]" :cy="Y" :r="aktif === i + 1 ? R + 4 : R" fill="#0b0c0f"
                :stroke="aktif > i ? '#5eead4' : '#343842'" :stroke-width="aktif === i + 1 ? 3 : 2" class="titik" />
        <circle v-if="aktif > i + 1" :cx="X[i]" :cy="Y" :r="R" fill="#5eead4" class="titik" />
        <path v-if="aktif > i + 1" :d="`M${X[i] - 8} ${Y + 1} L${X[i] - 2} ${Y + 7} L${X[i] + 9} ${Y - 6}`" stroke="#0b0c0f" stroke-width="3.2" />
        <text v-else :x="X[i]" :y="Y + 5" text-anchor="middle" :fill="aktif === i + 1 ? '#5eead4' : '#6b7280'"
              style="font-size:14px;font-weight:800;font-family:'JetBrains Mono'">{{ g.no }}</text>
        <text :x="X[i]" :y="Y + 44" text-anchor="middle" :fill="aktif >= i + 1 ? '#f4f5f7' : '#6b7280'"
              style="font-size:15px;font-weight:700;font-family:'Plus Jakarta Sans'">{{ g.nama }}</text>
      </g>

      <!-- kesalahan paling umum: lompat melewati Data -->
      <g class="muncul" :class="{ ya: k >= 6 && !cetak }">
        <path :d="lompat" stroke="#a0a6b1" stroke-width="2" stroke-dasharray="5 6" />
        <path :d="`M${X[1] - 8} ${Y - R - 16} L${X[1]} ${Y - R - 5} L${X[1] + 7} ${Y - R - 17}`" stroke="#a0a6b1" stroke-width="2" />
      </g>
    </svg>

    <!-- panel fokus: satu pertanyaan besar -->
    <div v-if="!cetak" class="fokus">
      <Transition name="ganti" mode="out-in">
        <div v-if="k >= 6" key="salah" class="isi">
          <p class="besar biru">01</p>
          <div>
            <p class="pertanyaan">Kesalahan paling umum: <span class="biru">langsung memilih AI</span> sebelum datanya beres.</p>
            <p class="contoh">Mulai dari gerbang 01 — Data. Lima pertanyaan ini dipakai lagi di lembar kerja diskusi.</p>
          </div>
        </div>
        <div v-else-if="aktif > 0 && aktif <= 5" :key="aktif" class="isi">
          <p class="besar">{{ gerbang[aktif - 1].no }}</p>
          <div>
            <p class="nama">{{ gerbang[aktif - 1].nama }}</p>
            <p class="pertanyaan">{{ gerbang[aktif - 1].tanya }}</p>
            <p class="contoh"><span class="mint">Di Satu Etam:</span> {{ gerbang[aktif - 1].contoh }}</p>
          </div>
        </div>
      </Transition>
    </div>

    <!-- ekspor/PDF: daftar ringkas -->
    <div v-else class="ringkas">
      <div v-for="g in gerbang" :key="g.no"><span class="no">{{ g.no }}</span><b>{{ g.nama }}</b><span>{{ g.tanya }}</span></div>
    </div>
  </div>
</template>

<style scoped>
.maju { transition: stroke-dashoffset .7s cubic-bezier(.45,.05,.25,1); }
.titik { transition: r .3s ease, stroke .3s ease; }
.muncul { opacity: 0; transition: opacity .5s ease; }
.muncul.ya { opacity: 1; }

.fokus { margin-top: 34px; border-top: 1px solid #24272e; padding-top: 26px; min-height: 230px; }
.isi { display: grid; grid-template-columns: 150px 1fr; gap: 24px; align-items: start; }
.isi p { margin: 0; }
.besar { font-weight: 800; font-size: 96px; line-height: .9; letter-spacing: -0.04em; color: #5eead4; }
.besar.biru { color: #4ea1f3; }
.nama { font-family: 'JetBrains Mono', monospace; font-size: 15px; color: #5eead4; margin-bottom: 8px !important; }
.pertanyaan { font-weight: 800; font-size: 34px; line-height: 1.18; letter-spacing: -0.02em; color: #f4f5f7; }
.contoh { font-size: 19px; line-height: 1.45; color: #a0a6b1; margin-top: 16px !important; max-width: 820px; }
.mint { color: #5eead4; font-weight: 700; }
.biru { color: #4ea1f3; }
.ganti-enter-active, .ganti-leave-active { transition: opacity .25s ease, transform .3s cubic-bezier(.2,.7,.2,1); }
.ganti-enter-from { opacity: 0; transform: translateY(12px); }
.ganti-leave-to { opacity: 0; transform: translateY(-8px); }

.ringkas { margin-top: 26px; border-top: 1px solid #24272e; }
.ringkas > div { display: grid; grid-template-columns: 48px 170px 1fr; gap: 16px; padding: 11px 0; border-bottom: 1px solid #24272e; font-size: 18px; align-items: baseline; }
.ringkas .no { font-family: 'JetBrains Mono', monospace; color: #5eead4; font-size: 15px; }
.ringkas span:last-child { color: #a0a6b1; }
@media (prefers-reduced-motion: reduce) { .maju, .titik, .muncul, .ganti-enter-active, .ganti-leave-active { transition: none; } }
</style>
