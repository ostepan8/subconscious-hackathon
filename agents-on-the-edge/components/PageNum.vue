<script setup lang="ts">
defineProps<{ n: string }>();
</script>

<template>
  <div class="slide-footrule"></div>
  <div class="slide-wordmark">subconscious.dev × ACM · hackathon</div>
  <div class="slide-pagenum">{{ n }} / 15</div>
</template>
