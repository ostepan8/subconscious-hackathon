<script setup lang="ts">
defineProps<{ n?: string }>();
</script>

<template>
  <div class="end">
    <DotGrid />
    <div class="end__mark">
      <OrbitLogo :size="300" />
    </div>
    <div class="end__body">
      <slot />
    </div>
    <PageNum v-if="n" :n="n" />
  </div>
</template>

<style scoped>
.end {
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  overflow: hidden;
}
.end__mark {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  opacity: 0.15;
  z-index: 1;
}
.end__body {
  position: relative;
  z-index: 2;
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 32px;
  align-items: center;
}
.end__body :deep(h2) {
  font-family: var(--font-display);
  font-size: 172px;
  font-weight: 800;
  letter-spacing: -0.04em;
  line-height: 0.92;
  color: var(--text);
}
.end__body :deep(h2 em) {
  font-style: normal;
  color: var(--orange);
}
.end__body :deep(p) {
  font-size: 28px;
  color: var(--text-muted);
  max-width: 60ch;
}
</style>
