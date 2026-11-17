<script setup>
// Sampul: titik-titik data acak menyatu ke AI → diperiksa manusia (sebagian ditolak, jatuh) → keputusan berdenyut.
// Berulang terus (SMIL). Mode ekspor / reduced-motion: hanya kerangka diam.
import { useNav } from '@slidev/client'
const { isPrintMode } = useNav()
const gerak = !isPrintMode.value && !(typeof window !== 'undefined' && window.matchMedia?.('(prefers-reduced-motion: reduce)').matches)

const X = { ai: 470, periksa: 730, putus: 1010 }, Y = 80
const ys = [14, 36, 58, 102, 124, 146, 26, 136]
// tiap partikel: jalur, durasi, jeda mulai, ditolak di "Periksa"?
const partikel = Array.from({ length: 16 }, (_, i) => {
  const y = ys[i % ys.length]
  const tolak = i % 5 === 3
  const awal = `M${10 + (i * 37) % 120},${y} C260,${y} 330,${Y} ${X.ai},${Y}`
  const d = tolak
    ? `${awal} L${X.periksa},${Y} Q${X.periksa + 30},${Y} ${X.periksa + 40},${Y + 70}`
    : `${awal} L${X.putus},${Y}`
  return { d, tolak, dur: 6, begin: -(i * 0.375) }
})
</script>

<template>
  <svg class="alur-sampul" viewBox="0 0 1120 160" aria-hidden="true">
    <!-- jalur dasar -->
    <path v-for="y in ys.slice(0, 6)" :key="y" :d="`M10,${y} C260,${y} 330,${Y} ${X.ai},${Y}`" class="jalur" />
    <line :x1="X.ai" :y1="Y" :x2="X.putus" :y2="Y" class="jalur kuat" />

    <!-- simpul -->
    <circle :cx="X.ai" :cy="Y" r="22" class="simpul" />
    <text :x="X.ai" :y="Y + 5" class="huruf ai">AI</text>
    <rect :x="X.periksa - 18" :y="Y - 18" width="36" height="36" rx="8" class="simpul" />
    <path :d="`M${X.periksa - 7},${Y} l5,5 l9,-10`" class="centang" />
    <circle :cx="X.putus" :cy="Y" r="12" class="putus" />
    <circle v-if="gerak" :cx="X.putus" :cy="Y" r="12" class="denyut">
      <animate attributeName="r" values="12;34" dur="2s" repeatCount="indefinite" />
      <animate attributeName="opacity" values="0.7;0" dur="2s" repeatCount="indefinite" />
    </circle>

    <text x="10" y="158" class="label">data tersebar</text>
    <text :x="X.ai" :y="Y + 52" class="label tengah">AI merangkum</text>
    <text :x="X.periksa" :y="Y + 52" class="label tengah">manusia memeriksa</text>
    <text :x="X.putus" :y="Y + 52" class="label tengah">keputusan</text>

    <!-- partikel berjalan -->
    <template v-if="gerak">
      <circle v-for="(p, i) in partikel" :key="i" r="3.5" :class="p.tolak ? 'titik tolak' : 'titik'">
        <animateMotion :path="p.d" :dur="p.dur + 's'" :begin="p.begin + 's'" repeatCount="indefinite"
          calcMode="spline" keyTimes="0;1" keySplines="0.4 0 0.6 1" />
        <animate attributeName="opacity" :values="p.tolak ? '0;1;1;0' : '0;1;1;0'" keyTimes="0;0.08;0.85;1"
          :dur="p.dur + 's'" :begin="p.begin + 's'" repeatCount="indefinite" />
      </circle>
    </template>
  </svg>
</template>

<style scoped>
.alur-sampul { width: 100%; height: auto; display: block; overflow: visible; margin-bottom: 14px; }
.jalur { fill: none; stroke: var(--garis-kuat, #3a3f49); stroke-width: 1; }
.jalur.kuat { stroke: #3a3f49; stroke-width: 1.5; }
.simpul { fill: #0b0c0f; stroke: #f4f5f7; stroke-width: 1.5; }
.huruf { fill: #f4f5f7; text-anchor: middle; font-family: 'JetBrains Mono', monospace; font-weight: 700; }
.ai { font-size: 15px; }
.centang { fill: none; stroke: #5eead4; stroke-width: 2.2; stroke-linecap: round; stroke-linejoin: round; }
.putus { fill: #5eead4; }
.denyut { fill: none; stroke: #5eead4; stroke-width: 1.5; }
.label { fill: #a0a6b1; font-family: 'JetBrains Mono', monospace; font-size: 13px; }
.label.tengah { text-anchor: middle; }
.titik { fill: #4ea1f3; }
.titik.tolak { fill: #a0a6b1; }
</style>
