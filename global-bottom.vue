<script setup>
// Latar hidup: jaringan titik tipis yang bergerak sangat pelan (kesan "simpul data").
// Sengaja samar (±10–20%) supaya mata tetap ke isi slide. Latar kertas/malam juga
// dilukis di sini, karena .slidev-layout dibuat transparan (lihat styles/index.css).
// Mode ekspor/PDF & prefers-reduced-motion: digambar sekali, tidak bergerak.
import { computed, onBeforeUnmount, onMounted, ref, watch } from 'vue'
import { injectLocal } from '@vueuse/core'

// Konteks Slidev (di mode ekspor disediakan per slide oleh PrintSlideClick lewat provideLocal).
const konteks = injectLocal('$$slidev-context')
const nav = computed(() => konteks.nav)
const fm = computed(() => nav.value.currentSlideRoute?.meta?.slide?.frontmatter || {})
const malam = computed(() => String(fm.value.class || '').includes('malam'))
const sampul = computed(() => fm.value.layout === 'cover')

const W = 1280, H = 720
const kanvas = ref(null)
const WARNA = {
  kertas: { bg: [11, 12, 15], titik: [148, 163, 184] }, // slide biasa: hitam pekat
  malam: { bg: [8, 14, 20], titik: [94, 234, 212] },   // slide pernyataan: sedikit kebiruan, titik mint
}

let ctx, raf, titik = [], campur = 0, target = 0, tampak = 0.1, tampakTarget = 0.1, terakhir = 0
const diam = typeof window !== 'undefined' && (
  window.matchMedia('(prefers-reduced-motion: reduce)').matches || nav.value.isPrintMode
)

// Pseudo-acak dengan benih tetap: pola sama setiap kali dibuka/diekspor.
function acak(benih) { return () => ((benih = (benih * 16807) % 2147483647) / 2147483647) }

function siapkan() {
  const r = acak(44)
  titik = Array.from({ length: 64 }, () => ({
    x: r() * W, y: r() * H,
    vx: (r() - 0.5) * 0.12, vy: (r() - 0.5) * 0.12,
    rad: 1 + r() * 1.2,
    mint: r() < 0.12, // sebagian kecil simpul berwarna mint
  }))
}

const lerp = (a, b, t) => a + (b - a) * t
const rgb = (c, a = 1) => `rgba(${c.map(Math.round).join(',')},${a})`

function gambar() {
  const bg = WARNA.kertas.bg.map((v, i) => lerp(v, WARNA.malam.bg[i], campur))
  const tt = WARNA.kertas.titik.map((v, i) => lerp(v, WARNA.malam.titik[i], campur))
  ctx.fillStyle = rgb(bg)
  ctx.fillRect(0, 0, W, H)
  const jarak = 140
  for (let i = 0; i < titik.length; i++) {
    const a = titik[i]
    for (let j = i + 1; j < titik.length; j++) {
      const b = titik[j]
      const d = Math.hypot(a.x - b.x, a.y - b.y)
      if (d < jarak) {
        ctx.strokeStyle = rgb(tt, tampak * 0.55 * (1 - d / jarak))
        ctx.lineWidth = 0.8
        ctx.beginPath(); ctx.moveTo(a.x, a.y); ctx.lineTo(b.x, b.y); ctx.stroke()
      }
    }
  }
  for (const p of titik) {
    ctx.fillStyle = p.mint ? `rgba(94,234,212,${tampak * 3})` : rgb(tt, tampak * 1.6)
    ctx.beginPath(); ctx.arc(p.x, p.y, p.mint ? p.rad + 0.6 : p.rad, 0, Math.PI * 2); ctx.fill()
  }
}

function gerak(dt) {
  for (const p of titik) {
    p.x += p.vx * dt; p.y += p.vy * dt
    if (p.x < -20) p.x = W + 20; if (p.x > W + 20) p.x = -20
    if (p.y < -20) p.y = H + 20; if (p.y > H + 20) p.y = -20
  }
}

function putar(t) {
  raf = requestAnimationFrame(putar)
  if (t - terakhir < 33) return // ±30 fps cukup untuk gerak selambat ini
  const dt = Math.min((t - terakhir) / 16.7, 4)
  terakhir = t
  campur += (target - campur) * 0.08
  tampak += (tampakTarget - tampak) * 0.05
  gerak(dt)
  gambar()
}

function setTarget() {
  target = malam.value ? 1 : 0
  tampakTarget = sampul.value ? 0.2 : 0.13
}
watch([malam, sampul], () => { setTarget(); if (diam) { campur = target; tampak = tampakTarget; gambar() } })

onMounted(() => {
  const c = kanvas.value
  const dpr = Math.min(window.devicePixelRatio || 1, 2) * 1.5
  c.width = W * dpr; c.height = H * dpr
  ctx = c.getContext('2d'); ctx.scale(dpr, dpr)
  siapkan(); setTarget(); campur = target; tampak = tampakTarget
  if (diam) gambar()
  else raf = requestAnimationFrame(putar)
})
onBeforeUnmount(() => cancelAnimationFrame(raf))
</script>

<template>
  <canvas ref="kanvas" class="absolute inset-0" style="width: 100%; height: 100%; pointer-events: none" aria-hidden="true" />
</template>
