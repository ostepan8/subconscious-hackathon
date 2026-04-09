<script setup lang="ts">
defineProps<{ tag?: string; n?: string }>();
</script>

<template>
  <div class="centered">
    <Eyebrow v-if="tag" :index="n || ''" :label="tag" />
    <div class="centered__body">
      <slot />
    </div>
    <PageNum v-if="n" :n="n" />
  </div>
</template>

<style scoped>
.centered {
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  padding: 156px 112px 120px;
}
.centered__body {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 48px;
  text-align: center;
}
.centered__body :deep(h2) {
  font-family: var(--font-display);
  font-size: 96px;
  font-weight: 800;
  letter-spacing: -0.035em;
  line-height: 1;
  color: var(--text);
}
.centered__body :deep(p) {
  font-size: 24px;
  color: var(--text-muted);
  max-width: 56ch;
}
</style>
