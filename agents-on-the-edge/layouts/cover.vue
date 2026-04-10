<template>
  <div class="cover">
    <DotGrid />

    <div class="cover__grid">
      <div class="cover__orbit">
        <OrbitLogo :size="660" />
      </div>

      <div class="cover__copy">
        <div class="cover__eyebrow">
          <span class="dot"></span>
          <span>SUBCONSCIOUS × ACM · NORTHEASTERN</span>
          <span class="sep"></span>
          <span>{{ $slidev.configs.date || '2026 · 04 · 11' }}</span>
        </div>
        <slot />
        <div class="cover__qr">
          <span class="mono-tag">DISCORD</span>
          <img src="/assets/discord-qr.png" alt="Discord QR" />
          <a href="https://discord.gg/Ud7M5jXu" target="_blank" class="cover__qr-link mono">discord.gg/Ud7M5jXu</a>
        </div>
      </div>
    </div>

  </div>
</template>

<style scoped>
.cover {
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  overflow: hidden;
}

.cover__grid {
  position: relative;
  display: grid;
  grid-template-columns: 1.1fr 1.15fr;
  align-items: center;
  gap: 48px;
  max-width: 1720px;
  padding: 0 96px 80px;
  width: 100%;
  z-index: 2;
}

.cover__orbit {
  position: relative;
  display: grid;
  place-items: center;
  overflow: visible;
  margin-left: -24px;
}

.cover__eyebrow {
  display: flex;
  align-items: center;
  gap: 14px;
  font-family: var(--font-mono);
  font-size: 13px;
  color: var(--text-faint);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  margin-bottom: 36px;
  opacity: 0;
  animation: fade-up 720ms var(--ease-out) 300ms forwards;
}
.cover__eyebrow .dot {
  width: 6px; height: 6px; border-radius: 50%; background: var(--orange);
  box-shadow: 0 0 14px var(--orange-glow);
}
.cover__eyebrow .sep { width: 18px; height: 1px; background: var(--border-hi); }

.cover__copy :deep(h1) {
  font-family: var(--font-display);
  font-size: 124px;
  font-weight: 800;
  letter-spacing: -0.052em;
  line-height: 0.92;
  color: var(--text);
  opacity: 0;
  animation: fade-up 900ms var(--ease-out) 400ms forwards;
}

.cover__copy :deep(h1 em) {
  font-style: normal;
  color: var(--orange) !important;
  -webkit-text-fill-color: var(--orange) !important;
}

.cover__copy :deep(p) {
  margin-top: 28px;
  font-size: 22px;
  line-height: 1.55;
  color: var(--text-muted);
  max-width: 42ch;
  opacity: 0;
  animation: fade-up 900ms var(--ease-out) 600ms forwards;
}

.cover__qr {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 12px;
  margin-top: 36px;
  opacity: 0;
  animation: fade-up 900ms var(--ease-out) 750ms forwards;
}
.cover__qr .mono-tag { color: var(--text-faint); }
.cover__qr img {
  width: 340px;
  height: 340px;
  border-radius: 12px;
  border: 1px solid var(--border);
  image-rendering: pixelated;
}
.cover__qr-link {
  font-size: 18px;
  color: var(--text-muted);
  letter-spacing: 0.02em;
  transition: color var(--dur-fast) var(--ease-out);
}
.cover__qr-link:hover {
  color: var(--orange);
}

.cover__meta {
  position: absolute;
  left: 112px;
  right: 112px;
  bottom: 128px;
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: max-content;
  column-gap: 56px;
  padding-top: 18px;
  border-top: 1px solid var(--border);
  z-index: 3;
  opacity: 0;
  animation: fade-up 900ms var(--ease-out) 900ms forwards;
}
.cover__backers {
  position: absolute;
  left: 112px;
  right: 112px;
  bottom: 48px;
  padding-top: 18px;
  border-top: 1px solid var(--border);
  z-index: 3;
  opacity: 0;
  animation: fade-up 900ms var(--ease-out) 1200ms forwards;
}
.meta__row {
  display: flex;
  flex-direction: column;
  gap: 4px;
}
.meta__v {
  font-size: 14px;
  color: var(--text);
  letter-spacing: 0.04em;
}

@keyframes fade-up {
  from { opacity: 0; transform: translateY(14px); }
  to   { opacity: 1; transform: none; }
}
</style>
