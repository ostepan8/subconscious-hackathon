<!--
  IntegrationMarquee — infinite horizontal scroll of SDK + tool logos.
-->
<script setup lang="ts">
const logos = [
  { src: "/assets/integrations/python.svg",          label: "Python" },
  { src: "/assets/integrations/typescript.svg",      label: "TypeScript" },
  { src: "/assets/integrations/claude.svg",          label: "Claude" },
  { src: "/assets/integrations/exa.svg",             label: "Exa" },
  { src: "/assets/integrations/parallel-search.svg", label: "Parallel" },
  { src: "/assets/integrations/convex.svg",          label: "Convex" },
  { src: "/assets/integrations/e2b.svg",             label: "E2B" },
  { src: "/assets/integrations/browserbase.png",     label: "Browserbase" },
  { src: "/assets/integrations/notion.png",          label: "Notion" },
  { src: "/assets/integrations/slack.png",           label: "Slack" },
  { src: "/assets/integrations/bigquery.svg",        label: "BigQuery" },
  { src: "/assets/integrations/elasticsearch.svg",   label: "Elastic" },
  { src: "/assets/integrations/cursor.svg",          label: "Cursor" },
  { src: "/assets/integrations/nextjs.svg",          label: "Next.js" },
];
</script>

<template>
  <div class="marquee">
    <div class="marquee__track">
      <div class="marquee__cell" v-for="(l, i) in logos" :key="'a' + i">
        <img :src="l.src" :alt="l.label" />
        <span class="mono">{{ l.label }}</span>
      </div>
      <div class="marquee__cell" v-for="(l, i) in logos" :key="'b' + i" aria-hidden="true">
        <img :src="l.src" :alt="l.label" />
        <span class="mono">{{ l.label }}</span>
      </div>
    </div>
    <div class="marquee__fade marquee__fade--l"></div>
    <div class="marquee__fade marquee__fade--r"></div>
  </div>
</template>

<style scoped>
.marquee {
  position: relative;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 12px;
  background: var(--surface);
  padding: 22px 0;
}
.marquee__track {
  display: flex;
  gap: 56px;
  width: max-content;
  animation: scroll 40s linear infinite;
}
.marquee__cell {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 0 8px;
  color: var(--text-muted);
  font-size: 14px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
.marquee__cell img {
  height: 28px;
  width: auto;
  filter: grayscale(1) brightness(1.2);
  opacity: 0.75;
}
.marquee__fade {
  position: absolute;
  top: 0; bottom: 0;
  width: 140px;
  pointer-events: none;
}
.marquee__fade--l { left: 0;  background: linear-gradient(90deg, var(--bg),    transparent); }
.marquee__fade--r { right: 0; background: linear-gradient(270deg, var(--bg),   transparent); }

@keyframes scroll {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}
</style>
