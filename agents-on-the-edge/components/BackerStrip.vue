<!--
  BackerStrip — a row of backer / university marks used on the cover.
-->
<script setup lang="ts">
const backers = [
  { src: "/assets/backers/nvidia.png",       label: "NVIDIA Inception" },
  { src: "/assets/backers/mit-csail.png",    label: "MIT CSAIL" },
  { src: "/assets/backers/e14.png",          label: "E14" },
  { src: "/assets/backers/underscore.png",   label: "Underscore VC" },
  { src: "/assets/backers/agentfund.png",    label: "Agent Fund" },
  { src: "/assets/backers/miracleplus.png",  label: "Miracle Plus" },
];
</script>

<template>
  <div class="strip">
    <div class="strip__label mono-tag">● BACKED BY</div>
    <div class="strip__row">
      <div class="strip__cell" v-for="(b, i) in backers" :key="i">
        <img :src="b.src" :alt="b.label" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.strip {
  display: flex;
  align-items: center;
  gap: 20px;
}
.strip__label { color: #fff; white-space: nowrap; }
.strip__row {
  display: inline-flex;
  align-items: center;
  gap: 32px;
  padding: 14px 28px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.12);
}
.strip__cell img {
  height: 28px;
  width: auto;
  opacity: 0.9;
  filter: brightness(1.3) contrast(1.1);
  transition: all var(--dur-fast) var(--ease-out);
}
.strip__cell:hover img { opacity: 1; filter: brightness(1.5); }
/* Agent Fund logo needs to be darker to contrast with backdrop */
.strip__cell:nth-child(5) img {
  filter: brightness(0.4) contrast(1.2);
  opacity: 1;
}
.strip__cell:nth-child(5):hover img { filter: brightness(0.5) contrast(1.2); }
</style>
