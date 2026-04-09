<!--
  AgentIdeaCard — compact card used in the agent ideas grid.
-->
<script setup lang="ts">
defineProps<{
  title: string;
  body: string;
  tag?: string;
}>();
</script>

<template>
  <div class="idea">
    <div class="idea__index mono">{{ tag || "·" }}</div>
    <h4 class="idea__title">{{ title }}</h4>
    <p class="idea__body">{{ body }}</p>
    <div class="idea__rule"></div>
  </div>
</template>

<style scoped>
.idea {
  position: relative;
  padding: 14px 16px 16px;
  border: 1px solid var(--border);
  border-radius: 10px;
  background: var(--surface);
  display: flex;
  flex-direction: column;
  gap: 5px;
  transition: all var(--dur-base) var(--ease-out);
  overflow: hidden;
}
.idea:hover {
  border-color: var(--orange);
  transform: translateY(-3px);
  box-shadow: 0 12px 24px rgba(0,0,0,0.35), 0 0 0 1px var(--orange);
}
.idea__index {
  font-size: 10px;
  color: var(--orange);
  letter-spacing: 0.2em;
  text-transform: uppercase;
}
.idea__title {
  font-family: var(--font-display);
  font-size: 16px;
  font-weight: 700;
  color: var(--text);
  letter-spacing: -0.01em;
  line-height: 1.15;
}
.idea__body {
  font-size: 12px;
  line-height: 1.4;
  color: var(--text-muted);
}
.idea__rule {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 2px;
  background: var(--orange);
  transform: scaleY(0);
  transform-origin: top;
  transition: transform var(--dur-base) var(--ease-out);
}
.idea:hover .idea__rule { transform: scaleY(1); }
</style>
