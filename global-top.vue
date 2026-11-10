<script setup>
// Footer berjalan: nama bagian (frontmatter `bagian`) + nomor halaman. Tidak tampil di sampul.
import { computed } from 'vue'
import { useNav } from '@slidev/client'

const { currentSlideRoute, currentPage, total } = useNav()
const fm = computed(() => currentSlideRoute.value?.meta?.slide?.frontmatter || {})
const malam = computed(() => String(fm.value.class || '').includes('malam'))
</script>

<template>
  <footer
    v-if="fm.layout !== 'cover'"
    class="absolute left-0 right-0 bottom-0 flex justify-between"
    :style="{
      padding: '0 80px 18px',
      fontFamily: `'IBM Plex Mono', monospace`,
      fontSize: '13px',
      color: malam ? '#a9acb6' : '#6b665c',
    }"
  >
    <span>SIMFONI ITK 2026<template v-if="fm.bagian"> · {{ fm.bagian }}</template></span>
    <span>{{ String(currentPage).padStart(2, '0') }} / {{ total }}</span>
  </footer>
</template>
