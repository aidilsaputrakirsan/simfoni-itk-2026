<script setup>
// SimpleQA (OpenAI, "Why language models hallucinate", Sep 2025; dari GPT-5 system card):
//   o4-mini            benar 24%, salah 75%  → tidak menjawab ±1%  (100 − 24 − 75)
//   gpt-5-thinking-mini benar 22%, salah 26% → tidak menjawab ±52% (100 − 22 − 26)
// Batang tumbuh saat slide dibuka; ekspor: langsung final.
import { ref, watch } from 'vue'
import { useIsSlideActive, useNav } from '@slidev/client'

const aktif = useIsSlideActive()
const { isPrintMode } = useNav()
const jalan = ref(isPrintMode.value)
watch(aktif, (a) => {
  if (isPrintMode.value) return
  jalan.value = false
  if (a) requestAnimationFrame(() => requestAnimationFrame(() => { jalan.value = true }))
}, { immediate: true })

const model = [
  { nama: 'o4-mini', catatan: 'hampir selalu menjawab', benar: 24, tidak: 1, salah: 75 },
  { nama: 'gpt-5-thinking-mini', catatan: 'berani bilang “tidak tahu”', benar: 22, tidak: 52, salah: 26 },
]
</script>

<template>
  <div class="ttt">
    <div class="legenda">
      <span><i class="b" /> benar</span><span><i class="t" /> tidak menjawab</span><span><i class="s" /> salah (halusinasi)</span>
    </div>
    <div v-for="(m, i) in model" :key="m.nama" class="model">
      <div class="atas"><b>{{ m.nama }}</b><span class="redup">{{ m.catatan }}</span></div>
      <div class="bar">
        <span class="b" :style="{ width: (jalan ? m.benar : 0) + '%', transitionDelay: i * 0.25 + 's' }">{{ m.benar }}%</span>
        <span class="t" :style="{ width: (jalan ? m.tidak : 0) + '%', transitionDelay: i * 0.25 + 0.15 + 's' }">{{ m.tidak >= 10 ? m.tidak + '%' : '' }}</span>
        <span class="s" :style="{ width: (jalan ? m.salah : 0) + '%', transitionDelay: i * 0.25 + 0.3 + 's' }">{{ m.salah }}%</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.ttt { width: 100%; }
.legenda { display: flex; gap: 22px; font-size: 14px; color: #a0a6b1; margin-bottom: 14px; }
.legenda i { display: inline-block; width: 12px; height: 12px; border-radius: 3px; vertical-align: -1px; margin-right: 6px; }
.model { margin-bottom: 18px; }
.atas { display: flex; gap: 12px; align-items: baseline; margin-bottom: 8px; font-size: 17px; }
.atas b { font-family: 'JetBrains Mono', monospace; font-weight: 600; color: #f4f5f7; }
.redup { color: #a0a6b1; font-size: 15px; }
.bar { display: flex; height: 40px; border-radius: 8px; overflow: hidden; background: #17191e; }
.bar > span { display: flex; align-items: center; padding-left: 10px; font-family: 'JetBrains Mono', monospace; font-size: 15px; font-weight: 600; white-space: nowrap; overflow: hidden; transition: width 1s cubic-bezier(.2,.7,.2,1); }
.b { background: #5eead4; color: #0b0c0f; }
.t { background: #3a3f4a; color: #e5e7eb; }
.s { background: #4ea1f3; color: #0b0c0f; }
@media (prefers-reduced-motion: reduce) { .bar > span { transition: none; } }
</style>
