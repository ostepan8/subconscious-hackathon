<!--
  TaskTree — hand-drawn SVG task decomposition.
  Edges animate on with stroke-dashoffset when the slide enters.
-->
<template>
  <div class="tree">
    <svg viewBox="0 0 680 380" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <linearGradient id="edge" x1="0" x2="1">
          <stop offset="0%"  stop-color="#FF5C28" stop-opacity="0.15"/>
          <stop offset="100%" stop-color="#FF5C28" stop-opacity="0.9"/>
        </linearGradient>
      </defs>

      <!-- edges (drawn first so they sit behind nodes) -->
      <g class="edges" fill="none" stroke="url(#edge)" stroke-width="1.5" stroke-linecap="round">
        <path d="M118 190 C 200 190, 200 100, 282 100"  style="--d:0ms"/>
        <path d="M118 190 C 200 190, 200 190, 282 190"  style="--d:140ms"/>
        <path d="M118 190 C 200 190, 200 280, 282 280"  style="--d:280ms"/>
        <path d="M414 100 C 470 100, 470 64,  538 64"   style="--d:420ms"/>
        <path d="M414 100 C 470 100, 470 136, 538 136"  style="--d:560ms"/>
        <path d="M414 190 C 470 190, 470 190, 538 190"  style="--d:700ms"/>
      </g>

      <!-- nodes -->
      <g class="nodes" fill="#FAFAF9">
        <g class="node node--task" style="--d:0ms">
          <rect x="12" y="166" width="106" height="48" rx="10"/>
          <text x="65" y="195" text-anchor="middle" class="label label--task">TASK</text>
        </g>

        <g class="node" style="--d:200ms">
          <rect x="282" y="76" width="132" height="48" rx="10"/>
          <text x="348" y="105" text-anchor="middle" class="label">subtask 1</text>
        </g>
        <g class="node" style="--d:340ms">
          <rect x="282" y="166" width="132" height="48" rx="10"/>
          <text x="348" y="195" text-anchor="middle" class="label">subtask 2</text>
        </g>
        <g class="node" style="--d:480ms">
          <rect x="282" y="256" width="132" height="48" rx="10"/>
          <text x="348" y="285" text-anchor="middle" class="label">subtask 3</text>
        </g>

        <g class="node node--leaf" style="--d:620ms">
          <rect x="538" y="42" width="128" height="44" rx="10"/>
          <text x="602" y="69" text-anchor="middle" class="label">subtask 1a</text>
        </g>
        <g class="node node--leaf" style="--d:720ms">
          <rect x="538" y="114" width="128" height="44" rx="10"/>
          <text x="602" y="141" text-anchor="middle" class="label">subtask 1b</text>
        </g>
        <g class="node node--leaf" style="--d:820ms">
          <rect x="538" y="168" width="128" height="44" rx="10"/>
          <text x="602" y="195" text-anchor="middle" class="label">subtask 2a</text>
        </g>
      </g>
    </svg>

    <div class="tree__result">
      <span class="mono-tag">FINAL RESULT</span>
      <span class="pulse"></span>
    </div>
  </div>
</template>

<style scoped>
.tree {
  position: relative;
  width: 100%;
}

svg { width: 100%; height: auto; display: block; }

.node rect {
  fill: var(--surface-2);
  stroke: var(--border-hi);
  stroke-width: 1;
  opacity: 0;
  transform: translateY(6px);
  animation: node-in 540ms var(--ease-out) forwards;
  animation-delay: var(--d);
}
.label {
  opacity: 0;
  animation: text-in 540ms var(--ease-out) forwards;
  animation-delay: calc(var(--d) + 60ms);
  letter-spacing: 0.04em;
  font-family: "Geist Mono", ui-monospace, monospace;
  font-size: 15px;
  font-weight: 500;
  fill: var(--text);
}
.label--task { font-size: 16px; font-weight: 700; fill: #0a0a0a; letter-spacing: 0.14em; }
.node--task rect { fill: var(--orange); stroke: var(--orange); }
.node--leaf rect { fill: var(--surface); }

.edges path {
  stroke-dasharray: 300;
  stroke-dashoffset: 300;
  animation: edge-draw 900ms var(--ease-out) forwards;
  animation-delay: var(--d);
}

.tree__result {
  margin-top: 24px;
  height: 64px;
  border-radius: 12px;
  background: linear-gradient(90deg, var(--orange), var(--orange-hi));
  color: #0a0a0a;
  font-family: var(--font-mono);
  font-weight: 600;
  letter-spacing: 0.18em;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 14px;
  position: relative;
  overflow: hidden;
  opacity: 0;
  animation: result-in 640ms var(--ease-out) 1100ms forwards;
  box-shadow: 0 0 0 1px rgba(255, 92, 40, 0.4), 0 24px 60px var(--orange-glow);
}
.pulse {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #0a0a0a;
  animation: pulse 2s var(--ease-in-out) infinite;
}

@keyframes node-in   { to { opacity: 1; transform: translateY(0); } }
@keyframes text-in   { to { opacity: 1; } }
@keyframes edge-draw { to { stroke-dashoffset: 0; } }
@keyframes result-in { to { opacity: 1; } }
@keyframes pulse {
  0%, 100% { transform: scale(1);   opacity: 1;   }
  50%      { transform: scale(1.4); opacity: 0.4; }
}
</style>
