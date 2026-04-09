<!--
  JudgingCard — oversized criterion card.
-->
<script setup lang="ts">
defineProps<{
  eyebrow: string;
  title: string;
  body: string;
  weight?: string;
  icon?: "brain" | "money";
}>();
</script>

<template>
  <div class="card">
    <div class="card__halo"></div>
    <div class="card__head">
      <span class="mono-tag">{{ eyebrow }}</span>
      <span v-if="weight" class="card__weight mono">{{ weight }}</span>
    </div>
    <h3 class="card__title">{{ title }}</h3>
    <p class="card__body">{{ body }}</p>
    <svg v-if="icon === 'brain'" class="card__icon" viewBox="0 0 64 64" fill="none">
      <path d="M22 10c-6 0-10 4-10 10v4c-3 2-4 5-4 8 0 4 3 7 7 7h1v7c0 5 4 9 9 9h12c5 0 9-4 9-9v-7h1c4 0 7-3 7-7 0-3-1-6-4-8v-4c0-6-4-10-10-10-3 0-5 1-7 3-2-2-4-3-7-3-3 0-5 1-7 3" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <path d="M24 24v4M40 24v4M32 30v8M28 46h8" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
    </svg>
    <svg v-if="icon === 'money'" class="card__icon" viewBox="0 0 64 64" fill="none">
      <rect x="6" y="16" width="52" height="32" rx="4" stroke="currentColor" stroke-width="2"/>
      <circle cx="32" cy="32" r="8" stroke="currentColor" stroke-width="2"/>
      <path d="M32 26v12M29 29h5a2 2 0 1 1 0 4h-4a2 2 0 1 0 0 4h5" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <circle cx="14" cy="32" r="2" fill="currentColor"/>
      <circle cx="50" cy="32" r="2" fill="currentColor"/>
    </svg>
  </div>
</template>

<style scoped>
.card {
  position: relative;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 18px;
  padding: 48px 44px 52px;
  min-height: 440px;
  display: flex;
  flex-direction: column;
  gap: 20px;
  overflow: hidden;
  transition: transform var(--dur-base) var(--ease-out), border-color var(--dur-base) var(--ease-out);
}
.card:hover {
  transform: translateY(-6px);
  border-color: var(--orange);
}
.card__halo {
  position: absolute;
  inset: -1px;
  background: radial-gradient(600px 200px at 50% -100px, var(--orange-wash), transparent 70%);
  opacity: 0.6;
  pointer-events: none;
}
.card__head {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.card__weight {
  font-size: 13px;
  color: var(--orange);
  letter-spacing: 0.1em;
}
.card__title {
  font-family: var(--font-display);
  font-size: 56px;
  font-weight: 800;
  line-height: 1.02;
  letter-spacing: -0.03em;
  color: var(--text);
}
.card__body {
  font-size: 22px;
  line-height: 1.5;
  color: var(--text-muted);
  max-width: 38ch;
}
.card__icon {
  position: absolute;
  right: 44px;
  bottom: 44px;
  width: 72px;
  height: 72px;
  color: var(--orange);
  opacity: 0.9;
}
</style>
