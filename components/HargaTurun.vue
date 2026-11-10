<script setup>
// Harga per 1 juta token (blended 3 input : 1 output) untuk kemampuan TETAP, sumbu Y logaritmik.
// - Setara GPT-3.5 (MMLU 64,8): Stanford AI Index 2025 — US$20 (Nov 2022) → US$0,07 (Okt 2024, Gemini 1.5 Flash-8B).
// - Setara GPT-4 (MMLU ≥ 86): Epoch AI, "LLM inference prices have fallen rapidly but unequally across tasks"
//   (12 Mar 2025) — GPT-4 US$37,50 (Mar 2023), GPT-4 Turbo US$15 (Nov 2023), Gemini 1.5 Pro US$2,19 (Mei 2024),
//   Gemini 2.0 Flash US$0,18 (Feb 2025).
// - Nov 2026: harga OpenRouter (10 Nov 2026) untuk model yang dipakai Satu Etam: DeepSeek V4 Flash US$0,11,
//   Qwen3.5-9B US$0,19, Qwen3-VL-30B US$0,26. Ditampilkan sebagai penanda terpisah, BUKAN bagian garis tren
//   (tidak ada sumber yang menyatakan kemampuannya "setara").
import { ref, watch } from 'vue'
import { useIsSlideActive, useNav } from '@slidev/client'

const W = 700, H = 380, pad = { l: 64, r: 20, t: 24, b: 44 }
const t0 = 2022.7, t1 = 2027.05, min = 0.04, max = 60
const x = (t) => pad.l + (t - t0) / (t1 - t0) * (W - pad.l - pad.r)
const y = (v) => pad.t + (Math.log10(max) - Math.log10(v)) / (Math.log10(max) - Math.log10(min)) * (H - pad.t - pad.b)

const gpt35 = [[2022.875, 20], [2024.79, 0.07]]
const gpt4 = [[2023.2, 37.5], [2023.85, 15], [2024.39, 2.19], [2025.1, 0.18]]
const satuEtam = { t: 2026.86, lo: 0.11, hi: 0.26 }

const jalur = (pts) => pts.map((p, i) => `${i ? 'L' : 'M'}${x(p[0]).toFixed(1)} ${y(p[1]).toFixed(1)}`).join(' ')
const panjang = (pts) => pts.slice(1).reduce((s, p, i) => s + Math.hypot(x(p[0]) - x(pts[i][0]), y(p[1]) - y(pts[i][1])), 0)
const pj35 = panjang(gpt35), pj4 = panjang(gpt4)
const gridY = [0.1, 1, 10]
const tahun = [2023, 2024, 2025, 2026]

// Animasi: garis "tergambar" saat slide dibuka, lalu label & penanda 2026 muncul. Ekspor: langsung final.
const aktif = useIsSlideActive()
const { isPrintMode } = useNav()
const jalan = ref(isPrintMode.value)
watch(aktif, (a) => {
  if (isPrintMode.value) return
  jalan.value = false
  if (a) requestAnimationFrame(() => requestAnimationFrame(() => { jalan.value = true }))
}, { immediate: true })
const rp = (v) => 'US$' + String(v).replace('.', ',')
</script>

<template>
  <svg :viewBox="`0 0 ${W} ${H}`" :width="W" :height="H" role="img"
       aria-label="Harga per satu juta token turun: setara GPT-3.5 dari 20 dolar ke 0,07 dolar; setara GPT-4 dari 37,5 dolar ke 0,18 dolar; model Satu Etam November 2026 0,11 sampai 0,26 dolar">
    <!-- grid -->
    <g v-for="g in gridY" :key="g">
      <line :x1="pad.l" :x2="W - pad.r" :y1="y(g)" :y2="y(g)" stroke="#343842" stroke-width="1" stroke-dasharray="2 5" />
      <text :x="pad.l - 10" :y="y(g) + 4" text-anchor="end" style="font-size:12px;font-family:'JetBrains Mono'" fill="#6b7280">{{ rp(g) }}</text>
    </g>
    <g v-for="th in tahun" :key="th">
      <line :x1="x(th)" :x2="x(th)" :y1="H - pad.b" :y2="H - pad.b + 5" stroke="#343842" />
      <text :x="x(th)" :y="H - 14" text-anchor="middle" style="font-size:12px;font-family:'JetBrains Mono'" fill="#6b7280">{{ th }}</text>
    </g>

    <!-- setara GPT-4 (biru) -->
    <path :d="jalur(gpt4)" stroke="#4ea1f3" stroke-width="3" fill="none" stroke-linecap="round" stroke-linejoin="round"
          class="garis" :class="{ jalan }" :style="{ strokeDasharray: pj4, strokeDashoffset: jalan ? 0 : pj4 }" />
    <circle v-for="(p, i) in gpt4" :key="'b' + i" :cx="x(p[0])" :cy="y(p[1])" r="4.5" fill="#4ea1f3" class="ujung" :class="{ jalan }" />
    <text :x="x(2023.2) + 10" :y="y(37.5) - 6" style="font-size:15px;font-weight:800;font-family:'Plus Jakarta Sans'" fill="#4ea1f3">{{ rp(37.5) }}</text>
    <text :x="x(2025.1) + 10" :y="y(0.18) - 8" style="font-size:15px;font-weight:800;font-family:'Plus Jakarta Sans'" fill="#4ea1f3" class="ujung" :class="{ jalan }">{{ rp(0.18) }}</text>

    <!-- setara GPT-3.5 (mint) -->
    <path :d="jalur(gpt35)" stroke="#5eead4" stroke-width="3" fill="none" stroke-linecap="round"
          class="garis" :class="{ jalan }" :style="{ strokeDasharray: pj35, strokeDashoffset: jalan ? 0 : pj35 }" />
    <circle :cx="x(gpt35[0][0])" :cy="y(20)" r="4.5" fill="#5eead4" />
    <circle :cx="x(gpt35[1][0])" :cy="y(0.07)" r="5.5" fill="#5eead4" class="ujung" :class="{ jalan }" />
    <text :x="x(gpt35[0][0]) - 4" :y="y(20) + 24" style="font-size:15px;font-weight:800;font-family:'Plus Jakarta Sans'" fill="#5eead4">{{ rp(20) }}</text>
    <text :x="x(gpt35[1][0]) - 10" :y="y(0.07) + 24" style="font-size:15px;font-weight:800;font-family:'Plus Jakarta Sans'" fill="#5eead4" class="ujung" :class="{ jalan }">{{ rp(0.07) }}</text>

    <!-- legenda -->
    <g style="font-size:14px;font-weight:700;font-family:'Plus Jakarta Sans'">
      <line :x1="W - 230" :x2="W - 206" :y1="pad.t + 6" :y2="pad.t + 6" stroke="#4ea1f3" stroke-width="3" stroke-linecap="round" />
      <text :x="W - 196" :y="pad.t + 11" fill="#4ea1f3">Setara GPT-4</text>
      <line :x1="W - 230" :x2="W - 206" :y1="pad.t + 30" :y2="pad.t + 30" stroke="#5eead4" stroke-width="3" stroke-linecap="round" />
      <text :x="W - 196" :y="pad.t + 35" fill="#5eead4">Setara GPT-3.5</text>
    </g>

    <!-- penanda Nov 2026: model Satu Etam (rentang harga) -->
    <g class="ujung lambat" :class="{ jalan }">
      <line :x1="x(satuEtam.t)" :x2="x(satuEtam.t)" :y1="y(satuEtam.hi)" :y2="y(satuEtam.lo)" stroke="#f4f5f7" stroke-width="10" stroke-linecap="round" />
      <text :x="x(satuEtam.t) - 14" :y="y(satuEtam.hi) - 34" text-anchor="end" style="font-size:14px;font-weight:700;font-family:'Plus Jakarta Sans'" fill="#f4f5f7">Nov 2026 · model Satu Etam</text>
      <text :x="x(satuEtam.t) - 14" :y="y(satuEtam.hi) - 15" text-anchor="end" style="font-size:14px;font-family:'JetBrains Mono'" fill="#a0a6b1">US$0,11–0,26</text>
    </g>
  </svg>
</template>

<style scoped>
.garis { transition: none; }
.garis.jalan { transition: stroke-dashoffset 1.6s cubic-bezier(.45,.05,.25,1) .3s; }
.ujung { opacity: 0; transition: none; }
.ujung.jalan { opacity: 1; transition: opacity .5s ease 1.7s; }
.ujung.lambat.jalan { transition-delay: 2.2s; }
</style>
