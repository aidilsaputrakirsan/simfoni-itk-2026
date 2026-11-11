<script setup>
// "Otak" AI = model bahasa yang menebak kata berikutnya. Peluang di sini ILUSTRASI (bukan data).
// Per klik (frontmatter slide: `clicks: 3`):
//   1 = kandidat kata berikutnya + peluangnya · 2 = model memilih yang paling mungkin, jawaban terdengar yakin
//   3 = kesimpulan: model tidak melihat data → menebak → halusinasi.
// Mode ekspor: semua tampil.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const kandidat = [
  { kata: 'Sepinggan Baru', p: 31 },
  { kata: 'Gunung Bahagia', p: 24 },
  { kata: 'Klandasan Ilir', p: 18 },
  { kata: '“saya tidak tahu”', p: 3, jujur: true },
]
</script>

<template>
  <div class="tebak">
    <div class="kiri">
      <p class="label">pertanyaan</p>
      <p class="gelembung">“Kelurahan mana yang lansianya paling banyak di Balikpapan?”</p>

      <p class="label" style="margin-top:22px">jawaban model, kata demi kata</p>
      <p class="jawaban">
        Kelurahan dengan lansia terbanyak adalah
        <span class="slot" :class="{ isi: k >= 2 }">{{ k >= 2 ? 'Sepinggan Baru' : '…' }}</span><span v-if="k >= 2">.</span>
      </p>
      <p class="yakin" :class="{ ya: k >= 2 }">Terdengar yakin — tanpa satu pun angka atau sumber.</p>
    </div>

    <div class="kanan" :class="{ ya: k >= 1 }">
      <p class="label">kata berikutnya yang paling mungkin <span class="ilustrasi">(ilustrasi)</span></p>
      <div v-for="(c, i) in kandidat" :key="c.kata" class="baris" :class="{ pilih: k >= 2 && i === 0, jujur: c.jujur }">
        <span class="kata">{{ c.kata }}</span>
        <span class="batang"><span :style="{ width: (k >= 1 ? c.p * 2.6 : 0) + '%', transitionDelay: i * 0.12 + 's' }" /></span>
        <span class="p mono">{{ c.p }}%</span>
      </div>
    </div>

    <div class="simpul" :class="{ ya: k >= 3 }">
      <p class="besar">Model tidak pernah melihat data lansia Balikpapan. <span class="biru">Ia menebak kata yang paling mungkin</span> — itulah halusinasi.</p>
      <p class="kecil">Karena itu di Satu Etam, AI hanya memilih analisis; <b>angkanya dihitung sistem dari data</b>.</p>
    </div>
  </div>
</template>

<style scoped>
.tebak { display: grid; grid-template-columns: 1fr 1fr; column-gap: 56px; row-gap: 28px; }
p { margin: 0; }
.label { font-family: 'JetBrains Mono', monospace; font-size: 14px; color: #5eead4; margin-bottom: 10px !important; }
.ilustrasi { color: #6b7280; }
.gelembung { font-weight: 600; font-size: 21px; line-height: 1.35; border: 1px solid #343842; border-radius: 18px 18px 18px 4px; padding: 14px 18px; background: #121419; }
.jawaban { font-weight: 700; font-size: 24px; line-height: 1.4; color: #f4f5f7; }
.slot { display: inline-block; min-width: 150px; border-bottom: 2px dashed #6b7280; color: #6b7280; transition: all .4s ease; }
.slot.isi { border-bottom-color: #4ea1f3; color: #4ea1f3; }
.yakin { font-size: 16px; color: #a0a6b1; margin-top: 10px !important; opacity: 0; transition: opacity .4s ease .3s; }
.yakin.ya { opacity: 1; }

.kanan { opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.kanan.ya { opacity: 1; transform: none; }
.baris { display: grid; grid-template-columns: 180px 1fr 52px; gap: 14px; align-items: center; padding: 10px 0; border-bottom: 1px solid #24272e; transition: background .3s ease; }
.kata { font-size: 18px; font-weight: 600; color: #e5e7eb; }
.batang { height: 12px; border-radius: 6px; background: #17191e; overflow: hidden; }
.batang > span { display: block; height: 100%; border-radius: 6px; background: #3a3f4a; transition: width .8s cubic-bezier(.2,.7,.2,1), background .3s ease; }
.p { text-align: right; font-size: 16px; color: #a0a6b1; }
.baris.pilih .kata, .baris.pilih .p { color: #4ea1f3; }
.baris.pilih .batang > span { background: #4ea1f3; }
.baris.jujur .kata { color: #6b7280; font-style: italic; font-weight: 500; }

.simpul { grid-column: 1 / -1; border-top: 1px solid #24272e; padding-top: 22px; opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
.simpul.ya { opacity: 1; transform: none; }
.besar { font-weight: 800; font-size: 28px; line-height: 1.25; letter-spacing: -0.02em; color: #f4f5f7; }
.biru { color: #4ea1f3; }
.kecil { font-size: 18px; color: #a0a6b1; margin-top: 10px !important; }
.kecil b { color: #5eead4; }
.mono { font-family: 'JetBrains Mono', monospace; }
@media (prefers-reduced-motion: reduce) { * { transition: none !important; } }
</style>
