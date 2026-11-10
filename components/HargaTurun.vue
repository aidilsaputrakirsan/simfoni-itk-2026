<script setup>
// Grafik lereng: harga per 1 juta token untuk kemampuan setara GPT-3.5 (Stanford AI Index 2025).
// Sumbu Y logaritmik supaya penurunan 280× terbaca, bukan sekadar garis jatuh ke nol.
const W = 620, H = 360, pad = { l: 70, r: 150, t: 30, b: 50 }
const min = 0.05, max = 30
const y = (v) => pad.t + (Math.log10(max) - Math.log10(v)) / (Math.log10(max) - Math.log10(min)) * (H - pad.t - pad.b)
const x1 = pad.l, x2 = W - pad.r
const grid = [0.1, 1, 10]
</script>

<template>
  <svg :viewBox="`0 0 ${W} ${H}`" :width="W" :height="H" role="img" aria-label="Harga turun dari 20 dolar menjadi 0,07 dolar per satu juta token">
    <g v-for="g in grid" :key="g">
      <line :x1="pad.l" :x2="W - pad.r" :y1="y(g)" :y2="y(g)" stroke="#cfc8b8" stroke-width="1" stroke-dasharray="2 4" />
      <text :x="pad.l - 12" :y="y(g) + 5" text-anchor="end" font-family="IBM Plex Mono" style="font-size:14px" fill="#6b665c">US${{ String(g).replace('.', ',') }}</text>
    </g>
    <line :x1="x1" :y1="y(20)" :x2="x2" :y2="y(0.07)" stroke="#a8361b" stroke-width="3" />
    <circle :cx="x1" :cy="y(20)" r="6" fill="#1c1b19" />
    <circle :cx="x2" :cy="y(0.07)" r="6" fill="#a8361b" />
    <text :x="x1 + 14" :y="y(20) - 10" font-family="Newsreader" style="font-size:28px" fill="#1c1b19">US$20</text>
    <text :x="x2 + 14" :y="y(0.07) + 9" font-family="Newsreader" style="font-size:28px" fill="#a8361b">US$0,07</text>
    <text :x="x1" :y="H - 16" text-anchor="middle" font-family="IBM Plex Mono" style="font-size:14px" fill="#6b665c">Nov 2022</text>
    <text :x="x2" :y="H - 16" text-anchor="middle" font-family="IBM Plex Mono" style="font-size:14px" fill="#6b665c">Okt 2024</text>
  </svg>
</template>
