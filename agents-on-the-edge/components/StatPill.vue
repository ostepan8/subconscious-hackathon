<!--
  StatPill — small inline metric chip.
-->
<script setup lang="ts">
defineProps<{ label: string; value: string }>();
</script>

<template>
  <span class="pill">
    <span class="pill__label mono">{{ label }}</span>
    <span class="pill__sep"></span>
    <span class="pill__value mono">{{ value }}</span>
  </span>
</template>

<style scoped>
.pill {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 6px 12px;
  border-radius: 999px;
  background: var(--surface-2);
  border: 1px solid var(--border);
  font-family: var(--font-mono);
  font-size: 12px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}
.pill__label { color: var(--text-faint); }
.pill__sep   { width: 1px; height: 10px; background: var(--border-hi); }
.pill__value { color: var(--orange); }
</style>
