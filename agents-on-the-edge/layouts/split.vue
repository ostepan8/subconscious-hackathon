<script setup lang="ts">
defineProps<{
  tag?: string;
  n?: string;
  heading?: string;
  kicker?: string;
}>();
</script>

<template>
  <div class="split">
    <Eyebrow v-if="tag" :index="n || ''" :label="tag" />

    <div class="split__grid">
      <div class="split__left">
        <div class="kicker mono-tag" v-if="kicker">{{ kicker }}</div>
        <h2 v-if="heading" class="split__title" v-html="heading"></h2>
        <div class="split__copy">
          <slot name="left" />
        </div>
      </div>
      <div class="split__right">
        <slot name="right" />
      </div>
    </div>

    <PageNum v-if="n" :n="n" />
  </div>
</template>

<style scoped>
.split {
  position: absolute;
  inset: 0;
  padding: 156px 112px 120px;
}
.split__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 96px;
  height: 100%;
  align-items: center;
}

.kicker {
  margin-bottom: 18px;
  color: var(--orange);
  opacity: 0;
  animation: up 520ms var(--ease-out) 100ms forwards;
}

.split__title {
  font-family: var(--font-display);
  font-size: 82px;
  font-weight: 800;
  line-height: 1;
  letter-spacing: -0.035em;
  color: var(--text);
  margin: 0 0 32px;
  opacity: 0;
  animation: up 720ms var(--ease-out) 180ms forwards;
}
.split__title :deep(em) {
  font-style: normal;
  color: var(--orange);
}
.split__copy {
  opacity: 0;
  animation: up 720ms var(--ease-out) 320ms forwards;
}
.split__copy :deep(p) {
  font-size: 24px;
  line-height: 1.55;
  color: var(--text-muted);
  max-width: 52ch;
  margin-bottom: 18px;
}
.split__copy :deep(strong) { color: var(--text); font-weight: 600; }
.split__copy :deep(ul) { list-style: none; padding: 0; margin: 0; }
.split__copy :deep(li) {
  position: relative;
  font-size: 22px;
  color: var(--text-muted);
  padding: 10px 0 10px 24px;
  line-height: 1.45;
}
.split__copy :deep(li::before) {
  content: "";
  position: absolute;
  left: 0;
  top: 22px;
  width: 8px;
  height: 1px;
  background: var(--orange);
}

.split__right {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 24px;
}

@keyframes up { to { opacity: 1; transform: none; } }
</style>
