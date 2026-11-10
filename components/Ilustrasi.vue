<script setup>
// Ilustrasi line-art kecil: garis terang, sudut bulat, isian mint seperlunya.
// jenis: 'latih' (klaster chip GPU) · 'server' (rak server + unduh model) · 'api' (aplikasi ⇄ cloud)
defineProps({ jenis: String, lebar: { type: Number, default: 150 } })
const g = '#e5e7eb', m = '#5eead4'
</script>

<template>
  <svg :width="lebar" :height="lebar * 0.56" viewBox="0 0 150 84" fill="none" :stroke="g" stroke-width="2.4"
       stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
    <template v-if="jenis === 'latih'">
      <g v-for="(c, i) in [[8,6],[46,6],[84,6],[8,44],[46,44],[84,44]]" :key="i">
        <rect :x="c[0]" :y="c[1]" width="30" height="30" rx="7" />
        <rect :x="c[0] + 9" :y="c[1] + 9" width="12" height="12" rx="3" :fill="i % 2 === 0 ? m : 'none'" :stroke="i % 2 === 0 ? m : g" />
      </g>
      <path d="M38 21h8M76 21h8M38 59h8M76 59h8M23 36v8M61 36v8M99 36v8" :stroke="m" />
      <path d="M124 20h18M124 42h18M124 64h18" opacity=".5" />
    </template>

    <template v-else-if="jenis === 'server'">
      <rect x="40" y="10" width="100" height="18" rx="5" />
      <rect x="40" y="33" width="100" height="18" rx="5" />
      <rect x="40" y="56" width="100" height="18" rx="5" />
      <circle cx="52" cy="19" r="3" :fill="m" :stroke="m" /><circle cx="52" cy="42" r="3" :fill="m" :stroke="m" /><circle cx="52" cy="65" r="3" :fill="m" :stroke="m" />
      <path d="M100 19h28M100 42h28M100 65h28" opacity=".55" />
      <path d="M14 8v34M4 32l10 10 10-10" :stroke="m" />
      <rect x="2" y="50" width="24" height="24" rx="5" />
      <path d="M8 59h12M8 65h8" opacity=".6" />
    </template>

    <template v-else>
      <rect x="4" y="16" width="56" height="54" rx="8" />
      <path d="M4 28h56" />
      <circle cx="12" cy="22" r="1.6" :fill="g" /><circle cx="18" cy="22" r="1.6" :fill="g" /><circle cx="24" cy="22" r="1.6" :fill="g" />
      <rect x="12" y="38" width="34" height="8" rx="4" :fill="m" :stroke="m" />
      <path d="M12 56h26" opacity=".55" />
      <path d="M100 52h34a12 12 0 0 0 0-24 18 18 0 0 0-34-6 14 14 0 0 0 0 30z" />
      <path d="M66 38h24M84 32l6 6-6 6" :stroke="m" />
      <path d="M90 58H66M72 52l-6 6 6 6" opacity=".6" />
    </template>
  </svg>
</template>
