<!--
  BrowserFrame — macOS-ish browser chrome around an image.
-->
<script setup lang="ts">
defineProps<{
  src: string;
  url?: string;
  alt?: string;
}>();
</script>

<template>
  <figure class="frame">
    <header class="frame__chrome">
      <span class="frame__dot frame__dot--r"></span>
      <span class="frame__dot frame__dot--y"></span>
      <span class="frame__dot frame__dot--g"></span>
      <div class="frame__url" v-if="url">
        <span class="faint mono">{{ url }}</span>
      </div>
    </header>
    <img :src="src" :alt="alt || 'screenshot'" />
  </figure>
</template>

<style scoped>
.frame {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  overflow: hidden;
  box-shadow: var(--shadow-card);
  margin: 0;
  transform: translateY(16px);
  opacity: 0;
  animation: frame-in 700ms var(--ease-out) 180ms forwards;
}
.frame__chrome {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 14px 18px;
  border-bottom: 1px solid var(--border);
  background: var(--surface-2);
}
.frame__dot {
  width: 11px;
  height: 11px;
  border-radius: 50%;
}
.frame__dot--r { background: #FF5F57; }
.frame__dot--y { background: #FFBD2E; }
.frame__dot--g { background: #28C840; }
.frame__url {
  margin-left: 18px;
  padding: 6px 14px;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 6px;
  font-size: 12px;
  letter-spacing: 0.02em;
}
.faint { color: var(--text-faint); }
img { display: block; width: 100%; height: auto; }

@keyframes frame-in { to { opacity: 1; transform: none; } }
</style>
