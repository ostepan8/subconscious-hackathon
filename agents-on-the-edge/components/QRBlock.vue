<!--
  QRBlock — framed QR container with caption + URL.
  Generates the QR via the qrserver API at build-time (no runtime dep).
  For offline builds, users can drop a PNG into /public/assets/qr/.
-->
<script setup lang="ts">
const props = defineProps<{
  data: string;
  caption?: string;
  src?: string;
}>();

const qrSrc =
  props.src ??
  `https://api.qrserver.com/v1/create-qr-code/?size=520x520&margin=0&bgcolor=14141a&color=F5F5F7&data=${encodeURIComponent(props.data)}`;
</script>

<template>
  <figure class="qr">
    <div class="qr__frame">
      <img :src="qrSrc" alt="QR code" />
      <div class="qr__scan"></div>
    </div>
    <figcaption class="qr__caption">
      <span class="mono-tag" v-if="caption">{{ caption }}</span>
      <a :href="data" target="_blank" class="qr__url">{{ data }}</a>
    </figcaption>
  </figure>
</template>

<style scoped>
.qr { margin: 0; display: flex; flex-direction: column; align-items: center; gap: 18px; }
.qr__frame {
  position: relative;
  padding: 22px;
  background: var(--surface-2);
  border: 1px solid var(--border);
  border-radius: 18px;
  box-shadow: var(--shadow-card);
  overflow: hidden;
}
.qr__frame img {
  display: block;
  width: 320px;
  height: 320px;
  image-rendering: pixelated;
}
.qr__scan {
  position: absolute;
  left: 22px;
  right: 22px;
  height: 2px;
  top: 22px;
  background: linear-gradient(90deg, transparent, var(--orange), transparent);
  animation: scan 2.6s var(--ease-in-out) infinite;
  box-shadow: 0 0 24px var(--orange-glow);
}
.qr__caption {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
}
.qr__url {
  font-family: var(--font-mono);
  font-size: 16px;
  color: var(--text-muted);
  letter-spacing: 0.02em;
  text-decoration: none;
  transition: color var(--dur-fast) var(--ease-out);
}
.qr__url:hover {
  color: var(--orange);
}
@keyframes scan {
  0%   { transform: translateY(0);     opacity: 0; }
  10%  {                                opacity: 1; }
  90%  {                                opacity: 1; }
  100% { transform: translateY(316px); opacity: 0; }
}
</style>
