<script setup>
// Angka yang menghitung naik saat slide dibuka (mis. 280×). Mode ekspor: langsung angka akhir.
import { ref, watch } from 'vue'
import { useIsSlideActive, useNav } from '@slidev/client'

const props = defineProps({
  sampai: { type: Number, required: true },
  akhiran: { type: String, default: '' },
  durasi: { type: Number, default: 1400 },
})
const aktif = useIsSlideActive()
const { isPrintMode } = useNav()
const nilai = ref(isPrintMode.value ? props.sampai : 0)
let raf

watch(aktif, (a) => {
  cancelAnimationFrame(raf)
  if (!a || isPrintMode.value) { nilai.value = isPrintMode.value ? props.sampai : 0; return }
  const mulai = performance.now()
  const langkah = (t) => {
    const p = Math.min((t - mulai) / props.durasi, 1)
    nilai.value = Math.round(props.sampai * (1 - Math.pow(1 - p, 3)))
    if (p < 1) raf = requestAnimationFrame(langkah)
  }
  raf = requestAnimationFrame(langkah)
}, { immediate: true })
</script>

<template>
  <span class="mono-angka">{{ nilai }}{{ akhiran }}</span>
</template>

<style scoped>
.mono-angka { font-variant-numeric: tabular-nums; }
</style>
