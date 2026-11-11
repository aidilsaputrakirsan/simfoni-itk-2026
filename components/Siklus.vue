<script setup>
// Tiga pelajaran sebagai SATU siklus kerja, bukan tiga kartu:
// Data rapi → (AI) → manusia memeriksa → (keputusan) → diukur → hasil ukur memperbaiki data.
// Terungkap per klik (frontmatter slide: `clicks: 4`):
//   1 = titik Data · 2 = garis + "AI" + titik Periksa · 3 = garis + "keputusan" + titik Ukur · 4 = panah balik.
// Mode ekspor: semua tampil.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const W = 1120, Y = 150
const X = [W / 6, W / 2, (W * 5) / 6] // pusat tiga kolom
const R = 34
const seg = (a, b) => ({ x1: X[a] + R + 6, x2: X[b] - R - 6 })
const s1 = seg(0, 1), s2 = seg(1, 2)
const pj1 = s1.x2 - s1.x1, pj2 = s2.x2 - s2.x1
// panah balik: lengkung di atas, dari Ukur kembali ke Data
const balik = `M${X[2]} ${Y - R - 8} C ${X[2]} ${Y - 150}, ${X[0]} ${Y - 150}, ${X[0]} ${Y - R - 12}`
const pjBalik = 1250

const langkah = [
  { no: '01', judul: 'Mulai dari data, bukan dari AI', ket: 'Rapikan data di sumbernya. AI tidak bisa memperbaiki data yang tidak ada.' },
  { no: '02', judul: 'AI membantu, manusia memutuskan', ket: 'Tentukan di titik mana manusia wajib memeriksa — sebelum sistemnya dibangun.' },
  { no: '03', judul: 'Ukur dengan angka yang bisa dicek', ket: 'Waktu, biaya, ketepatan sasaran — dan catat setiap pemakaian.' },
]
</script>

<template>
  <div class="siklus" :style="{ width: W + 'px' }">
    <svg :width="W" :height="Y + R + 14" :viewBox="`0 0 ${W} ${Y + R + 14}`" fill="none" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <!-- jejak samar seluruh alur -->
      <line :x1="X[0]" :x2="X[2]" :y1="Y" :y2="Y" stroke="#24272e" stroke-width="2" stroke-dasharray="3 7" />

      <!-- garis 1 → 2, dengan label AI -->
      <line :x1="s1.x1" :x2="s1.x2" :y1="Y" :y2="Y" stroke="#5eead4" stroke-width="3"
            class="gambar" :style="{ strokeDasharray: pj1, strokeDashoffset: k >= 2 ? 0 : pj1 }" />
      <g class="muncul tunda" :class="{ ya: k >= 2 }">
        <rect :x="W / 3 - 26" :y="Y - 15" width="52" height="30" rx="15" fill="#0b0c0f" stroke="#5eead4" stroke-width="2" />
        <text :x="W / 3" :y="Y + 5" text-anchor="middle" fill="#5eead4" style="font-size:14px;font-weight:800;font-family:'Plus Jakarta Sans'">AI</text>
      </g>

      <!-- garis 2 → 3, dengan label keputusan -->
      <line :x1="s2.x1" :x2="s2.x2" :y1="Y" :y2="Y" stroke="#5eead4" stroke-width="3"
            class="gambar" :style="{ strokeDasharray: pj2, strokeDashoffset: k >= 3 ? 0 : pj2 }" />
      <g class="muncul tunda" :class="{ ya: k >= 3 }">
        <rect :x="(W * 2) / 3 - 56" :y="Y - 15" width="112" height="30" rx="15" fill="#0b0c0f" stroke="#4ea1f3" stroke-width="2" />
        <text :x="(W * 2) / 3" :y="Y + 5" text-anchor="middle" fill="#4ea1f3" style="font-size:14px;font-weight:800;font-family:'Plus Jakarta Sans'">keputusan</text>
      </g>

      <!-- panah balik: ukur → data -->
      <path :d="balik" stroke="#4ea1f3" stroke-width="2.5" class="gambar lambat"
            :style="{ strokeDasharray: pjBalik, strokeDashoffset: k >= 4 ? 0 : pjBalik }" />
      <g class="muncul tunda-lama" :class="{ ya: k >= 4 }">
        <path :d="`M${X[0] - 9} ${Y - R - 24} L${X[0]} ${Y - R - 10} L${X[0] + 9} ${Y - R - 24}`" stroke="#4ea1f3" stroke-width="2.5" />
        <text :x="W / 2" :y="Y - 88" text-anchor="middle" fill="#4ea1f3" style="font-size:15px;font-weight:700;font-family:'Plus Jakarta Sans'">hasil ukur memperbaiki data — lalu siklus berulang</text>
      </g>

      <!-- titik henti -->
      <g v-for="(x, i) in X" :key="i" class="muncul" :class="{ ya: k >= i + 1 }">
        <circle :cx="x" :cy="Y" :r="R" fill="#0b0c0f" :stroke="k >= i + 1 ? '#e5e7eb' : '#343842'" stroke-width="2.4" />
        <!-- 1: data (baris-baris rapi) -->
        <g v-if="i === 0" stroke="#e5e7eb" stroke-width="2.4">
          <path :d="`M${x - 14} ${Y - 9}h28M${x - 14} ${Y}h28M${x - 14} ${Y + 9}h18`" />
          <circle :cx="x + 13" :cy="Y + 9" r="3" fill="#5eead4" stroke="#5eead4" />
        </g>
        <!-- 2: manusia memeriksa (centang) -->
        <path v-else-if="i === 1" :d="`M${x - 13} ${Y + 1} L${x - 4} ${Y + 10} L${x + 14} ${Y - 10}`" stroke="#5eead4" stroke-width="3.4" />
        <!-- 3: ukur (batang naik) -->
        <g v-else stroke="#e5e7eb" stroke-width="2.4">
          <path :d="`M${x - 13} ${Y + 12}V${Y + 2}M${x} ${Y + 12}V${Y - 5}M${x + 13} ${Y + 12}V${Y - 12}`" />
          <path :d="`M${x - 16} ${Y + 14}h32`" stroke="#5eead4" />
        </g>
      </g>
    </svg>

    <div class="teks">
      <div v-for="(l, i) in langkah" :key="l.no" class="muncul-html" :class="{ ya: k >= i + 1 }">
        <p class="no">{{ l.no }}</p>
        <p class="judul">{{ l.judul }}</p>
        <p class="ket">{{ l.ket }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.gambar { transition: stroke-dashoffset .9s cubic-bezier(.45,.05,.25,1); }
.gambar.lambat { transition-duration: 1.4s; }
.muncul { opacity: 0; transition: opacity .45s ease; }
.muncul.ya { opacity: 1; }
.muncul.tunda.ya { transition-delay: .55s; }
.muncul.tunda-lama.ya { transition-delay: 1.1s; }

.teks { display: grid; grid-template-columns: repeat(3, 1fr); gap: 40px; margin-top: 14px; text-align: center; }
.muncul-html { opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.muncul-html.ya { opacity: 1; transform: none; }
.teks p { margin: 0; }
.teks .no { font-family: 'JetBrains Mono', monospace; font-size: 14px; color: #5eead4; margin-bottom: 6px; }
.teks .judul { font-weight: 800; font-size: 24px; line-height: 1.2; letter-spacing: -0.015em; color: #f4f5f7; }
.teks .ket { font-size: 17px; line-height: 1.45; color: #a0a6b1; margin-top: 10px; padding: 0 12px; }
@media (prefers-reduced-motion: reduce) {
  .gambar, .muncul, .muncul-html { transition: none; }
}
</style>
