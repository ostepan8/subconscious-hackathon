<script setup lang="ts">
defineProps<{ tag?: string; n?: string }>();
</script>

<template>
  <div class="section">
    <DotGrid />
    <Eyebrow v-if="tag" :index="n || ''" :label="tag" />
    <div class="section__body">
      <slot />
    </div>
    <PageNum v-if="n" :n="n" />
  </div>
</template>

<style scoped>
.section {
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  overflow: hidden;
}
.section__body {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 40px;
  text-align: center;
  z-index: 2;
}
.section__body :deep(h2) {
  font-family: var(--font-display);
  font-size: 156px;
  font-weight: 800;
  letter-spacing: -0.04em;
  line-height: 0.95;
  color: var(--text);
  opacity: 0;
  animation: in 900ms var(--ease-out) 200ms forwards;
}
.section__body :deep(h2 em) {
  font-style: normal;
  color: var(--orange);
  -webkit-text-fill-color: var(--orange);
}
.section__body :deep(p) {
  font-size: 28px;
  color: var(--text-muted);
  max-width: 60ch;
  opacity: 0;
  animation: in 900ms var(--ease-out) 420ms forwards;
}
@keyframes in { to { opacity: 1; transform: none; } }
</style>
