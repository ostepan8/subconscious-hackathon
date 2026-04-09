<!--
  ScheduleRail — vertical timeline with an animated tick.
-->
<script setup lang="ts">
interface Slot {
  time: string;
  label: string;
  detail?: string;
}
defineProps<{ slots: Slot[] }>();
</script>

<template>
  <div class="rail">
    <div class="rail__line"></div>
    <div class="rail__fill"></div>
    <div class="rail__item" v-for="(s, i) in slots" :key="i" :style="{ '--d': (i * 140) + 'ms' }">
      <div class="rail__dot"></div>
      <div class="rail__time mono">{{ s.time }}</div>
      <div class="rail__body">
        <div class="rail__label">{{ s.label }}</div>
        <div class="rail__detail" v-if="s.detail">{{ s.detail }}</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.rail {
  position: relative;
  padding-left: 40px;
  display: grid;
  grid-template-rows: repeat(5, auto);
  row-gap: 32px;
}
.rail__line,
.rail__fill {
  position: absolute;
  left: 11px;
  top: 12px;
  bottom: 44px;
  width: 1px;
}
.rail__line { background: var(--border); }
.rail__fill {
  background: linear-gradient(180deg, var(--orange), var(--orange-lo));
  transform-origin: top;
  animation: rail-fill 1400ms var(--ease-out) 400ms forwards;
  transform: scaleY(0);
  box-shadow: 0 0 16px var(--orange-glow);
}

.rail__item {
  position: relative;
  display: grid;
  grid-template-columns: 128px 1fr;
  column-gap: 32px;
  align-items: baseline;
  opacity: 0;
  transform: translateX(-12px);
  animation: item-in 540ms var(--ease-out) forwards;
  animation-delay: var(--d);
}
.rail__dot {
  position: absolute;
  left: -34px;
  top: 14px;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--bg);
  border: 2px solid var(--orange);
  box-shadow: 0 0 0 4px var(--bg), 0 0 16px var(--orange-glow);
}
.rail__time {
  font-family: var(--font-mono);
  font-size: 22px;
  font-weight: 600;
  color: var(--orange);
  letter-spacing: 0.04em;
}
.rail__label {
  font-family: var(--font-display);
  font-size: 28px;
  font-weight: 600;
  color: var(--text);
  line-height: 1.2;
}
.rail__detail {
  font-family: var(--font-mono);
  font-size: 13px;
  color: var(--text-faint);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  margin-top: 4px;
}

@keyframes rail-fill { to { transform: scaleY(1); } }
@keyframes item-in   { to { opacity: 1; transform: none; } }
</style>
