<script setup>
// Slide "Aturan main ditulis ke dalam sistem": lima gerbang dari slide "Lima pertanyaan" (LimaGerbang.vue),
// kini DIJAWAB oleh keputusan desain Satu Etam. Per klik (frontmatter slide: `clicks: 5`): gerbang ke-n
// dicentang dan jawabannya muncul di bawahnya. Mode ekspor: semua tampil. Isi = fakta di CLAUDE.md.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const gerbang = [
  { no: '01', nama: 'Data', jawab: ['Data dinas lebih dari dua tahun diberi tanda “data lama”'] },
  { no: '02', nama: 'Peran AI', jawab: ['Angka dihitung sistem', 'Sumber selalu ditampilkan'] },
  { no: '03', nama: 'Tata kelola', jawab: ['AI membaca, manusia memeriksa dan menyimpan', 'Semua aplikasi lewat satu gerbang AI (Myst-Core)'] },
  { no: '04', nama: 'Etika & privasi', jawab: ['Ke AI hanya angka agregat — tanpa nama, NIK, kontak, iuran', 'Penyedia wajib zero data retention; tanpa itu, ditolak'] },
  { no: '05', nama: 'Dampak', jawab: ['Setiap pemakaian AI tercatat lengkap dengan biayanya'] },
]
const W = 1120, Y = 34, R = 22
const X = gerbang.map((_, i) => (W / 5) * (i + 0.5))
const pj = X[4] - X[0]
const maju = computed(() => (k.value <= 1 ? 0 : X[Math.min(k.value, 5) - 1] - X[0]))
</script>

<template>
  <div class="gt" :style="{ width: W + 'px' }">
    <svg :width="W" :height="Y + R + 8" :viewBox="`0 0 ${W} ${Y + R + 8}`" fill="none" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <line :x1="X[0]" :x2="X[4]" :y1="Y" :y2="Y" stroke="#24272e" stroke-width="2" stroke-dasharray="3 7" />
      <line :x1="X[0]" :x2="X[4]" :y1="Y" :y2="Y" stroke="#5eead4" stroke-width="3" class="maju" :style="{ strokeDasharray: pj, strokeDashoffset: pj - maju }" />
      <g v-for="(g, i) in gerbang" :key="g.no">
        <circle :cx="X[i]" :cy="Y" :r="R" :fill="k > i ? '#5eead4' : '#0b0c0f'" :stroke="k > i ? '#5eead4' : '#343842'" stroke-width="2" class="titik" />
        <path v-if="k > i" :d="`M${X[i] - 8} ${Y + 1} L${X[i] - 2} ${Y + 7} L${X[i] + 9} ${Y - 6}`" stroke="#0b0c0f" stroke-width="3.2" />
        <text v-else :x="X[i]" :y="Y + 5" text-anchor="middle" fill="#6b7280" style="font-size:14px;font-weight:800;font-family:'JetBrains Mono'">{{ g.no }}</text>
      </g>
    </svg>

    <div class="kolom5">
      <div v-for="(g, i) in gerbang" :key="g.no" class="jawab" :class="{ ya: k > i }">
        <p class="nama">{{ g.nama }}</p>
        <p v-for="j in g.jawab" :key="j" class="butir">{{ j }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.maju { transition: stroke-dashoffset .7s cubic-bezier(.45,.05,.25,1); }
.titik { transition: fill .3s ease, stroke .3s ease; }
.kolom5 { display: grid; grid-template-columns: repeat(5, 1fr); gap: 0; margin-top: 14px; }
.jawab { padding: 0 16px; text-align: center; border-left: 1px solid #24272e; }
.jawab:first-child { border-left: none; }
.jawab p { margin: 0; }
.nama { font-weight: 800; font-size: 19px; color: #6b7280; margin-bottom: 14px !important; transition: color .3s ease; }
.jawab.ya .nama { color: #f4f5f7; }
.butir { font-size: 16px; line-height: 1.4; color: #a0a6b1; padding: 10px 0; border-top: 1px solid #24272e;
  opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.jawab.ya .butir { opacity: 1; transform: none; }
.jawab.ya .butir:nth-of-type(3) { transition-delay: .15s; }
@media (prefers-reduced-motion: reduce) { .maju, .titik, .nama, .butir { transition: none; } }
</style>
