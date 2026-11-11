<script setup>
// Bingkai rekaman/tangkapan layar aplikasi (taruh file di public/).
// Urutan: video (bila ada) → gambar → bingkai putus-putus berisi petunjuk.
// Video: tanpa suara, berulang, otomatis jalan selama slide ini tampil; berhenti & kembali ke awal
// saat pindah slide. Mode ekspor/PDF: yang tampil gambar (src), bukan video.
import { computed, ref, watch } from 'vue'
import { useIsSlideActive, useNav } from '@slidev/client'

const props = defineProps({
  src: String,    // gambar, mis. "/baca-kk.png" — juga jadi poster & cadangan video
  video: String,  // video, mis. "/baca-kk.mp4" (opsional)
  label: String,
  tinggi: { type: Number, default: 380 },
  pas: { type: String, default: 'cover' }, // object-fit: cover | contain
  zoom: { type: Number, default: 1 },      // perbesar bagian tengah-atas (mis. 1.35 bila rekaman bermargin lebar)
})
// path "/x.png" → ikut base deploy (GitHub Pages: /simfoni-itk-2026/)
const base = (p) => p?.startsWith('/') ? import.meta.env.BASE_URL + p.slice(1) : p
const url = computed(() => base(props.src))
const urlVideo = computed(() => base(props.video))

const aktif = useIsSlideActive()
const { isPrintMode } = useNav()
const videoGagal = ref(false)
const gambarGagal = ref(false)
const vid = ref(null)
const pakaiVideo = computed(() => props.video && !videoGagal.value && !isPrintMode.value)

watch([aktif, vid], ([a, v]) => {
  if (!v) return
  if (a) {
    v.currentTime = 0
    v.play().catch(() => {}) // muted → autoplay diizinkan browser
  } else {
    v.pause()
    v.currentTime = 0
  }
}, { immediate: true })

const bingkai = computed(() => ({
  height: props.tinggi + 'px', overflow: 'hidden',
  border: '1px solid #343842', borderRadius: '14px', background: '#121419',
}))
const gaya = computed(() => ({
  width: '100%', height: '100%', objectFit: props.pas, objectPosition: 'top', display: 'block',
  transform: props.zoom !== 1 ? `scale(${props.zoom})` : undefined, transformOrigin: 'top center',
}))
</script>

<template>
  <figure style="margin: 0">
    <div v-if="pakaiVideo || !gambarGagal" :style="bingkai">
      <video v-if="pakaiVideo" ref="vid" :src="urlVideo" :poster="gambarGagal ? undefined : url"
             muted loop playsinline preload="auto" :style="gaya" @error="videoGagal = true" />
      <img v-else :src="url" :alt="label" :style="gaya" @error="gambarGagal = true">
    </div>
    <div v-else class="flex items-center justify-center text-center mono"
         :style="{ height: tinggi + 'px', border: '1px dashed #343842', borderRadius: '14px', color: '#6b7280', fontSize: '15px', padding: '24px', background: '#121419' }">
      rekaman belum ada<br>{{ label }}<br>→ simpan sebagai public{{ video || src }}
    </div>
    <figcaption class="redup" style="font-size: 14px; margin-top: 6px">{{ label }}</figcaption>
  </figure>
</template>
