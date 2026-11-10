<script setup>
// Bingkai tangkapan layar aplikasi. Taruh file di folder public/ (mis. public/tanya-data.png).
// Selama file belum ada, tampil bingkai garis putus berisi keterangan apa yang perlu difoto.
import { ref } from 'vue'

defineProps({
  src: String,
  label: String,
  tinggi: { type: Number, default: 380 },
})
const gagal = ref(false)
</script>

<template>
  <figure style="margin: 0">
    <img v-if="!gagal" :src="src" :alt="label" @error="gagal = true"
         :style="{ width: '100%', height: tinggi + 'px', objectFit: 'cover', objectPosition: 'top', border: '1px solid #1c1b19' }">
    <div v-else class="flex items-center justify-center text-center mono"
         :style="{ height: tinggi + 'px', border: '1px dashed #6b665c', color: '#6b665c', fontSize: '15px', padding: '24px', background: '#ebe6da' }">
      tangkapan layar belum ada<br>{{ label }}<br>→ simpan sebagai public{{ src }}
    </div>
    <figcaption class="redup" style="font-size: 14px; margin-top: 6px">{{ label }}</figcaption>
  </figure>
</template>
