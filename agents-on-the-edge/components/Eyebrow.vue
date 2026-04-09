<script setup lang="ts">
defineProps<{
  index: string;
  label: string;
}>();
</script>

<template>
  <div class="slide-eyebrow">
    <span>{{ index }}</span>
    <span class="faint">/</span>
    <span>{{ label }}</span>
  </div>
</template>

<style scoped>
.slide-eyebrow { gap: 12px; }
.faint { color: var(--border-hi); }
</style>
