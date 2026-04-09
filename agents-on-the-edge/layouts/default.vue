<script setup lang="ts">
defineProps<{
  tag?: string;
  n?: string;
}>();
</script>

<template>
  <div class="slide">
    <Eyebrow v-if="tag" :index="n || ''" :label="tag" />
    <div class="slide__body">
      <slot />
    </div>
    <PageNum v-if="n" :n="n" />
  </div>
</template>

<style scoped>
.slide {
  position: absolute;
  inset: 0;
  padding: 160px 112px 120px;
}
.slide__body {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.slide :deep(h2) {
  font-family: var(--font-display);
  font-size: 96px;
  font-weight: 800;
  letter-spacing: -0.035em;
  line-height: 1;
  color: var(--text);
  margin-bottom: 40px;
  opacity: 0;
  transform: translateY(10px);
  animation: enter-h 720ms var(--ease-out) 120ms forwards;
}
.slide :deep(h2 em) {
  font-style: normal;
  color: var(--orange);
}
.slide :deep(p) {
  font-size: 26px;
  line-height: 1.55;
  color: var(--text-muted);
  max-width: 60ch;
}
.slide :deep(strong) {
  color: var(--text);
  font-weight: 600;
}

@keyframes enter-h {
  to { opacity: 1; transform: none; }
}
</style>
