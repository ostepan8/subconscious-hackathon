<!--
  ReasoningTree — 1:1 port of the website's landing tree demo.

  Source files (copied verbatim from the monorepo):
    apps/web/components/landing/AgentDemo.tsx
    apps/web/components/tree/TreeViewLanding.tsx

  The website demo renders a grid where odd columns are nodes
  (1fr) and even columns are connection cells (0.2fr). Each node
  is a white-on-light-orange card with:
    - a bold muted-gray title (text-xs)
    - an optional tool-use chip (border-primary/20 bg-primary/10)
    - a prominent h-[12px] bar at 70% brand orange as the
      conclusion indicator

  The sample data matches the website's `output1` trace
  ("Find 5 slurm experts in the Boston Area") so the deck and the
  marketing site visualize the exact same run.
-->
<script setup lang="ts">
type Cell =
  | null
  | { kind: "node"; title: string; tool?: string; conclusion: boolean }
  | {
      kind: "conn";
      up?: boolean;
      down?: boolean;
      left?: boolean;
      right?: boolean;
    };

// 4 node columns (max depth = 3) → 8 grid columns total.
// Columns: [rail][node][conn][node][conn][node][conn][node]
const TOTAL_COLS = 8;
const empty = (): Cell[] => Array(TOTAL_COLS).fill(null);

// Each row maps 1:1 to TreeViewLanding's buildRows output for the
// sample data. See apps/web/components/landing/AgentDemo.tsx :: output1
const grid: Cell[][] = [
  // --- Task 1 ---
  (() => {
    const r = empty();
    r[0] = { kind: "conn", up: true, down: true, right: true };
    r[1] = { kind: "node", title: "Task",     conclusion: true };
    r[2] = { kind: "conn", left: true, right: true, down: true };
    r[3] = { kind: "node", title: "Subtask",  conclusion: true };
    r[4] = { kind: "conn", left: true, right: true };
    r[5] = { kind: "node", title: "Tool Use", tool: "WebSearch",   conclusion: true };
    return r;
  })(),
  //  Task 1's second branch
  (() => {
    const r = empty();
    r[0] = { kind: "conn", up: true, down: true };
    r[2] = { kind: "conn", right: true, up: true };
    r[3] = { kind: "node", title: "Tool Use", tool: "PeopleSearch", conclusion: true };
    return r;
  })(),
  //  Task 1's Subtask second tool use
  (() => {
    const r = empty();
    r[0] = { kind: "conn", up: true, down: true };
    r[4] = { kind: "conn", right: true, up: true };
    r[5] = { kind: "node", title: "Tool Use", tool: "ExaCrawl",     conclusion: true };
    return r;
  })(),
  // --- Task 2 ---
  (() => {
    const r = empty();
    r[0] = { kind: "conn", up: true, right: true };
    r[1] = { kind: "node", title: "Task",     conclusion: true };
    r[2] = { kind: "conn", left: true, right: true };
    r[3] = { kind: "node", title: "Subtask",  conclusion: true };
    r[4] = { kind: "conn", left: true, right: true };
    r[5] = { kind: "node", title: "Tool Use", tool: "PageReader",   conclusion: true };
    return r;
  })(),
];

const tools = ["Parallel", "Exa", "Google", "LinkedIn"];
</script>

<template>
  <div class="card">
    <!-- header: prompt + tool chips -->
    <div class="card__header">
      <div class="header__prompt">
        <div class="label">Prompt</div>
        <div class="bar bar--full bar--gray"></div>
        <div class="bar bar--75 bar--gray"></div>
      </div>
      <div class="header__tools">
        <div
          class="tool-chip"
          v-for="(t, i) in tools"
          :key="t"
          :style="{ '--d': (i * 120 + 350) + 'ms' }"
        >
          {{ t }}
        </div>
      </div>
    </div>

    <!-- tree body -->
    <div class="tree">
      <div
        class="tree__row"
        v-for="(row, r) in grid"
        :key="r"
        :style="{ '--d': (700 + r * 220) + 'ms' }"
      >
        <template v-for="(cell, c) in row" :key="c">
          <!-- empty cell -->
          <div v-if="!cell" class="tree__cell"></div>

          <!-- node cell -->
          <div v-else-if="cell.kind === 'node'" class="tree__cell tree__cell--node">
            <div class="node">
              <div class="node__title">{{ cell.title }}</div>
              <div v-if="cell.tool" class="node__tool">
                <svg v-if="cell.title === 'Tool Use'" class="node__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <circle cx="12" cy="12" r="10"/>
                  <line x1="2" y1="12" x2="22" y2="12"/>
                  <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>
                </svg>
                <span>{{ cell.tool }}</span>
              </div>
              <div class="node__bar"></div>
            </div>
          </div>

          <!-- connection cell (2x2 grid with directional borders) -->
          <div v-else class="tree__cell tree__cell--conn">
            <div class="conn">
              <div :class="['conn__tl', { 'b-b': cell.left, 'b-r': cell.up }]"></div>
              <div :class="['conn__tr', { 'b-b': cell.right }]"></div>
              <div :class="['conn__bl', { 'b-r': cell.down }]"></div>
              <div class="conn__br"></div>
            </div>
          </div>
        </template>
      </div>
    </div>

    <!-- agent work summary -->
    <div class="summary">
      <div class="label label--accent">Agent Work Summary</div>
      <div class="bar bar--full bar--accent"></div>
      <div class="bar bar--75 bar--accent"></div>
      <div class="bar bar--full bar--accent"></div>
      <div class="bar bar--75 bar--accent"></div>
    </div>
  </div>
</template>

<style scoped>
/* ============================================================
   card
   ============================================================ */

.card {
  position: relative;
  background: rgba(255, 255, 255, 0.98);
  border: 1px solid hsl(0 0% 90%);
  border-radius: 6px;
  padding: 22px;
  width: 100%;
  min-width: 780px;
  color: hsl(20 14.3% 4.1%);
  font-family: var(--font-body);
  box-shadow:
    0 1px 0 rgba(255, 255, 255, 0.06) inset,
    0 40px 90px rgba(0, 0, 0, 0.55),
    0 12px 30px rgba(0, 0, 0, 0.4),
    0 0 0 1px rgba(255, 92, 40, 0.05);
  transform: perspective(1600px) rotateX(5deg) rotateY(-4deg) rotateZ(1.2deg);
  transform-origin: center;
  opacity: 0;
  animation: card-in 900ms var(--ease-out) 180ms forwards;
}
@keyframes card-in {
  to {
    opacity: 1;
    transform: perspective(1600px) rotateX(5deg) rotateY(-4deg) rotateZ(1.2deg)
      translateY(0);
  }
}

/* ============================================================
   header: prompt + tool chips
   ============================================================ */

.card__header {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  background: white;
  border: 1px solid hsl(0 0% 90%);
  border-radius: 4px;
  padding: 8px;
  margin-bottom: 14px;
}
.header__prompt {
  background: hsl(60 5% 96%);
  border-radius: 4px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.header__tools {
  padding: 6px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6px;
}

.tool-chip {
  background: hsl(60 5% 96%);
  border: 1px solid hsl(0 0% 90%);
  border-radius: 4px;
  padding: 6px 12px;
  font-size: 12px;
  font-weight: 800;
  color: hsl(25 5% 45%);
  text-align: center;
  opacity: 0;
  transform: translateY(-4px);
  animation: fade-in-down 360ms var(--ease-out) forwards;
  animation-delay: var(--d);
}

.label {
  font-size: 11px;
  font-weight: 800;
  color: hsl(25 5% 45%);
}
.label--accent { color: hsl(15 100% 48%); }

/* ============================================================
   generic bar
   ============================================================ */

.bar {
  height: 12px;
  border-radius: 3px;
}
.bar--full { width: 100%; }
.bar--75   { width: 75%; }
.bar--gray { background: hsl(0 0% 82%); }
.bar--accent {
  background: hsla(15, 100%, 58%, 0.7);
}

/* ============================================================
   tree grid — cols mirror TreeViewLanding's dynamic grid
     [conn] [node] [conn] [node] [conn] [node] [conn] [node]
   ============================================================ */

.tree {
  position: relative;
}
.tree__row {
  display: grid;
  grid-template-columns:
    0.2fr 1fr 0.2fr 1fr 0.2fr 1fr 0.2fr 1fr;
  width: 100%;
  min-height: 72px;
  opacity: 0;
  transform: translateX(-6px);
  animation: fade-in-left 420ms var(--ease-out) forwards;
  animation-delay: var(--d);
}
.tree__cell {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 72px;
  padding: 10px 0;
}

/* ============================================================
   node card — THIS is the hero element, match the website 1:1
   ============================================================ */

.node {
  width: 100%;
  min-height: 60px;
  background: hsla(15, 100%, 58%, 0.05);
  border: 1px solid hsla(15, 100%, 58%, 0.22);
  border-radius: 4px;
  padding: 10px 12px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 7px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.04);
}
.node__title {
  font-size: 12px;
  font-weight: 800;
  color: hsl(25 5% 40%);
  line-height: 1;
}
.node__tool {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 5px 8px;
  background: hsla(15, 100%, 58%, 0.1);
  border: 1px solid hsla(15, 100%, 58%, 0.22);
  border-radius: 3px;
  font-size: 11px;
  font-weight: 600;
  color: hsl(15 78% 32%);
  width: fit-content;
  max-width: 100%;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.node__icon {
  width: 11px;
  height: 11px;
  stroke-width: 2;
  color: hsl(15 78% 32%);
  flex-shrink: 0;
}
.node__bar {
  height: 12px;
  width: 100%;
  border-radius: 3px;
  background: hsla(15, 100%, 58%, 0.7);
}

/* ============================================================
   connection cell — 2x2 grid of quadrants, each with optional
   top/right borders to compose L-shaped connectors
   ============================================================ */

.conn {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  width: 100%;
  height: 100%;
}
.conn > div { width: 100%; height: 100%; }
.b-b { border-bottom: 2px solid hsl(0 0% 64%); }
.b-r { border-right: 2px solid hsl(0 0% 64%); }

/* ============================================================
   summary footer
   ============================================================ */

.summary {
  margin-top: 16px;
  padding: 12px 14px 14px;
  background: hsla(15, 100%, 58%, 0.05);
  border: 1px solid hsla(15, 100%, 58%, 0.32);
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  gap: 6px;
  opacity: 0;
  transform: translateY(6px);
  animation: fade-in-up 640ms var(--ease-out) 2400ms forwards;
}

/* ============================================================
   keyframes
   ============================================================ */

@keyframes fade-in-down {
  to { opacity: 1; transform: none; }
}
@keyframes fade-in-up {
  to { opacity: 1; transform: none; }
}
@keyframes fade-in-left {
  to { opacity: 1; transform: none; }
}
</style>
