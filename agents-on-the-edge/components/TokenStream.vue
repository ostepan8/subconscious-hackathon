<!--
  TokenStream — monospace terminal that types out lines.
  Used on the Python SDK walkthrough slide.
-->
<script setup lang="ts">
defineProps<{
  lines: { text: string; kind?: "prompt" | "comment" | "code" | "out" | "keyword" | "string" | "function" }[];
  title?: string;
  highlight?: boolean;
}>();

function highlightPython(text: string): string {
  // Tokenize to avoid double-highlighting
  const tokens: { text: string; type: string }[] = [];
  let remaining = text;

  while (remaining.length > 0) {
    // Check for strings first
    const stringMatch = remaining.match(/^("[^"]*"|'[^']*')/);
    if (stringMatch) {
      tokens.push({ text: stringMatch[0], type: 'string' });
      remaining = remaining.slice(stringMatch[0].length);
      continue;
    }

    // Check for keywords
    const keywordMatch = remaining.match(/^(from|import|def|class|return|if|else|elif|for|while|with|as|try|except|finally|raise|yield|lambda|and|or|not|in|is|None|True|False)\b/);
    if (keywordMatch) {
      tokens.push({ text: keywordMatch[0], type: 'keyword' });
      remaining = remaining.slice(keywordMatch[0].length);
      continue;
    }

    // Check for function calls
    const funcMatch = remaining.match(/^(\w+)(\s*\()/);
    if (funcMatch) {
      tokens.push({ text: funcMatch[1], type: 'function' });
      tokens.push({ text: funcMatch[2], type: 'plain' });
      remaining = remaining.slice(funcMatch[0].length);
      continue;
    }

    // Default: take one character
    tokens.push({ text: remaining[0], type: 'plain' });
    remaining = remaining.slice(1);
  }

  return tokens.map(t => {
    if (t.type === 'keyword') return `<span class="hl-keyword">${t.text}</span>`;
    if (t.type === 'string') return `<span class="hl-string">${t.text}</span>`;
    if (t.type === 'function') return `<span class="hl-function">${t.text}</span>`;
    return t.text;
  }).join('');
}
</script>

<template>
  <div class="stream">
    <header class="stream__bar">
      <span class="stream__dot r"></span>
      <span class="stream__dot y"></span>
      <span class="stream__dot g"></span>
      <span class="stream__title mono">{{ title || "python" }}</span>
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
        <span class="stream__text mono" v-if="highlight && l.kind === 'code'" v-html="highlightPython(l.text)"></span>
        <span class="stream__text mono" v-else>{{ l.text }}</span>
      </div>
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

.stream__text :deep(.hl-keyword) { color: #c678dd; }
.stream__text :deep(.hl-string) { color: #98c379; }
.stream__text :deep(.hl-function) { color: #61afef; }
.stream__text :deep(.hl-comment) { color: var(--text-faint); font-style: italic; }

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
