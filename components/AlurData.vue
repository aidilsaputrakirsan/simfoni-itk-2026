<script setup>
// Slide Satu Etam: apa yang terjadi pada DATA dari RT sampai meja Walikota.
// Data pribadi (nama, NIK, kontak, iuran) tertahan di "batas privasi"; yang lolos hanya yang bisa dijumlah.
// Per klik (frontmatter slide: `clicks: 4`):
//   1 = data di RT · 2 = batas privasi (data pribadi dicoret) + angka per wilayah · 3 = kota · 4 = keputusan.
// Fakta dari CLAUDE.md: 2 RT (RT 44 & 56) ±415 rumah; 91 indikator / 24 OPD; ke AI hanya agregat.
import { computed } from 'vue'
import { useSlideContext, useNav } from '@slidev/client'

const { $clicks } = useSlideContext()
const { isPrintMode } = useNav()
const k = computed(() => (isPrintMode.value ? 99 : $clicks.value))

const pribadi = ['nama', 'NIK', 'kontak', 'iuran']
const lolos = ['usia', 'jenis kelamin', 'pekerjaan', 'data balita']
const agregat = ['jumlah balita', 'jumlah lansia', 'pekerjaan per kategori', 'RT yang belum lapor']
</script>

<template>
  <div class="alur-data">
    <!-- 1. di RT -->
    <section :class="{ ya: k >= 1 }">
      <p class="tahap">di RT</p>
      <div class="chips">
        <span v-for="c in pribadi" :key="c" class="chip pribadi" :class="{ tertahan: k >= 2 }">{{ c }}</span>
        <span v-for="c in lolos" :key="c" class="chip">{{ c }}</span>
      </div>
      <p class="fakta"><b>2 RT</b> berjalan · <b>± 415</b> rumah</p>
      <p class="ket">RT 44 &amp; RT 56, Kel. Sepinggan Baru</p>
    </section>

    <!-- batas privasi -->
    <div class="batas" :class="{ ya: k >= 2 }">
      <span class="label">batas privasi</span>
    </div>

    <!-- 2. per wilayah -->
    <section :class="{ ya: k >= 2 }" class="tunda">
      <p class="tahap">per wilayah</p>
      <div class="chips">
        <span v-for="c in agregat" :key="c" class="chip mint">{{ c }}</span>
      </div>
      <p class="fakta">tanpa nama, NIK, kontak, iuran</p>
      <p class="ket">dijumlah per RT, kelurahan, kecamatan</p>
    </section>

    <span class="panah" :class="{ ya: k >= 3 }" aria-hidden="true"></span>

    <!-- 3. di kota -->
    <section :class="{ ya: k >= 3 }">
      <p class="tahap">di kota</p>
      <div class="chips">
        <span class="chip biru">+ indikator dinas</span>
        <span class="chip biru">Portal Satu Data</span>
      </div>
      <p class="fakta"><b>91</b> indikator · <b>24</b> OPD</p>
      <p class="ket">data &gt; 2 tahun ditandai “data lama”</p>
    </section>

    <span class="panah" :class="{ ya: k >= 4 }" aria-hidden="true"></span>

    <!-- 4. keputusan -->
    <section :class="{ ya: k >= 4 }">
      <p class="tahap">keputusan</p>
      <p class="tanya-kecil">“Kelurahan mana yang lansianya paling banyak?”</p>
      <p class="fakta">angka + sumber + saran program</p>
      <p class="ket">dihitung sistem, bukan dikarang AI</p>
    </section>
  </div>
</template>

<style scoped>
.alur-data { display: grid; grid-template-columns: 1.25fr 30px 1.05fr 34px 0.9fr 34px 1fr; align-items: start; column-gap: 8px; }
section { opacity: 0; transform: translateY(10px); transition: opacity .45s ease, transform .45s cubic-bezier(.2,.7,.2,1); }
section.ya { opacity: 1; transform: none; }
section.tunda.ya { transition-delay: .5s; }
section p { margin: 0; }
.tahap { font-family: 'JetBrains Mono', monospace; font-size: 15px; color: #5eead4; margin-bottom: 12px !important; }
.chips { display: flex; flex-wrap: wrap; gap: 9px; min-height: 150px; align-content: flex-start; }
.chip { font-size: 16px; line-height: 1; padding: 8px 13px; border-radius: 999px; border: 1px solid #343842; color: #e5e7eb; white-space: nowrap; transition: all .5s ease; }
.chip.pribadi { border-color: #6b7280; }
.chip.tertahan { color: #6b7280; border-style: dashed; text-decoration: line-through; opacity: .55; }
.chip.mint { border-color: #5eead4; color: #5eead4; }
.chip.biru { border-color: #4ea1f3; color: #4ea1f3; }
.fakta { font-weight: 800; font-size: 20px; line-height: 1.3; margin-top: 16px !important; color: #f4f5f7; }
.fakta b { color: #5eead4; }
.ket { font-size: 15px; color: #a0a6b1; margin-top: 4px !important; line-height: 1.4; }
.tanya-kecil { font-weight: 600; font-size: 18px; line-height: 1.35; border: 1px solid #343842; border-radius: 16px 16px 16px 4px; padding: 12px 16px; background: #121419; min-height: 150px; box-sizing: border-box; }

/* garis batas privasi */
.batas { position: relative; align-self: stretch; opacity: 0; transition: opacity .5s ease; }
.batas.ya { opacity: 1; }
.batas::before { content: ''; position: absolute; left: 50%; top: 0; bottom: 0; border-left: 2px dashed #5eead4; }
.batas .label { position: absolute; left: 50%; top: -30px; transform: translateX(-50%); white-space: nowrap; font-family: 'JetBrains Mono', monospace; font-size: 12px; color: #5eead4; background: #0b0c0f; padding: 0 4px; }

/* panah antar tahap */
.panah { position: relative; height: 150px; margin-top: 28px; opacity: 0; transition: opacity .4s ease; }
.panah.ya { opacity: 1; }
.panah::before { content: ''; position: absolute; left: 2px; right: 6px; top: 50%; border-top: 2px solid #4ea1f3; }
.panah::after { content: ''; position: absolute; right: 2px; top: calc(50% - 5px); border: solid #4ea1f3; border-width: 0 2px 2px 0; padding: 4px; transform: rotate(-45deg); }
@media (prefers-reduced-motion: reduce) { section, .batas, .panah, .chip { transition: none; } }
</style>
