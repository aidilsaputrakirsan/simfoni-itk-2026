<script setup>
// Batang horizontal skala logaritmik: biaya tiap anak tangga dalam rupiah.
// Angka: GPT-4 ±US$78 jt × Rp16.500; sewa 8 GPU ±Rp190 jt/bulan (batas bawah);
// 33 pemakaian awal API di Satu Etam ±US$0,008 ≈ Rp132.
const data = [
  { label: 'Melatih model sendiri', ket: 'sekali latih, setara GPT-4', nilai: 1.287e12, teks: '± Rp1,3 triliun' },
  { label: 'Server GPU sendiri', ket: '8 GPU H100, per bulan', nilai: 1.9e8, teks: '± Rp190–280 juta' },
  { label: 'API bayar per pemakaian', ket: '33 pemakaian awal Satu Etam', nilai: 132, teks: '< Rp150' },
]
const W = 1100, labelW = 330, barMax = W - labelW - 200
const lo = 1, hi = 13 // 10^1 .. 10^13
const lebar = (v) => ((Math.log10(v) - lo) / (hi - lo)) * barMax
</script>

<template>
  <div class="relative" :style="{ width: W + 'px' }">
    <div v-for="(d, i) in data" :key="d.label" v-click="i + 1"
         class="grid items-center" :style="{ gridTemplateColumns: `${labelW}px 1fr`, padding: '18px 0', borderTop: '1px solid #24272e' }">
      <div>
        <div style="font-size: 24px; line-height: 1.15; font-weight: 700; letter-spacing: -0.015em">{{ d.label }}</div>
        <div class="redup" style="font-size: 16px">{{ d.ket }}</div>
      </div>
      <div class="flex items-center gap-4">
        <div class="batang" :style="{ width: lebar(d.nilai) + 'px', height: '28px', borderRadius: '6px', background: i === 2 ? '#5eead4' : '#3a3f4a' }" />
        <span class="mono nilai" :style="{ fontSize: '22px', color: i === 2 ? '#5eead4' : '#f4f5f7', whiteSpace: 'nowrap' }">{{ d.teks }}</span>
      </div>
    </div>
    <div class="mono redup" style="font-size: 13px; border-top: 1px solid #24272e; padding-top: 10px">
      Skala logaritmik — setiap satu panjang batang yang sama berarti sepuluh kali lipat.
    </div>
  </div>
</template>

<style scoped>
/* Batang tumbuh dari kiri saat baris muncul (v-click), angkanya menyusul. */
.batang { transform-origin: left center; transition: transform 1s cubic-bezier(.2,.7,.2,1) .15s; }
.nilai { transition: opacity .4s ease .9s; }
.slidev-vclick-hidden .batang { transform: scaleX(0); transition: none; }
.slidev-vclick-hidden .nilai { opacity: 0; transition: none; }
</style>
