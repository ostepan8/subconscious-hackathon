<!--
  TokenStream — monospace terminal that types out lines.
  Used on the Python SDK walkthrough slide.
-->
<script setup lang="ts">
defineProps<{
  lines: { text: string; kind?: "prompt" | "comment" | "code" | "out" }[];
  title?: string;
}>();
</script>

<template>
  <div class="stream">
    <header class="stream__bar">
      <span class="stream__dot r"></span>
      <span class="stream__dot y"></span>
      <span class="stream__dot g"></span>
      <span class="stream__title mono">{{ title || "python — subconscious" }}</span>
    </header>
    <div class="stream__body">
      <div
        v-for="(l, i) in lines"
        :key="i"
        class="stream__line"
        :class="l.kind || 'code'"
        :style="{ '--d': (i * 140) + 'ms' }"
      >
        <span class="stream__gutter mono">{{ String(i + 1).padStart(2, '0') }}</span>
        <span class="stream__text mono">{{ l.text }}</span>
      </div>
      <div class="stream__cursor"></div>
    </div>
  </div>
</template>

<style scoped>
.stream {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
  box-shadow: var(--shadow-card);
  font-family: var(--font-mono);
}
.stream__bar {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 14px 18px;
  border-bottom: 1px solid var(--border);
  background: var(--surface-2);
}
.stream__dot { width: 11px; height: 11px; border-radius: 50%; }
.stream__dot.r { background: #FF5F57; }
.stream__dot.y { background: #FFBD2E; }
.stream__dot.g { background: #28C840; }
.stream__title {
  margin-left: 14px;
  font-size: 12px;
  color: var(--text-faint);
  letter-spacing: 0.08em;
}

.stream__body {
  padding: 24px 28px;
  font-size: 18px;
  line-height: 1.6;
  position: relative;
}
.stream__line {
  display: flex;
  gap: 22px;
  opacity: 0;
  transform: translateY(6px);
  animation: line-in 520ms var(--ease-out) forwards;
  animation-delay: var(--d);
}
.stream__gutter { color: var(--border-hi); min-width: 28px; }
.stream__text   { color: var(--text); white-space: pre; tab-size: 4; }
.stream__line.comment .stream__text { color: var(--text-faint); }
.stream__line.prompt  .stream__text { color: var(--orange); }
.stream__line.out     .stream__text { color: var(--green); }

.stream__cursor {
  position: absolute;
  bottom: 26px;
  left: 74px;
  width: 10px;
  height: 20px;
  background: var(--orange);
  animation: blink 1.1s steps(1) infinite, cursor-in 1ms 1800ms forwards;
  opacity: 0;
}

@keyframes line-in { to { opacity: 1; transform: none; } }
@keyframes blink { 50% { opacity: 0; } }
@keyframes cursor-in { to { opacity: 1; } }
</style>
