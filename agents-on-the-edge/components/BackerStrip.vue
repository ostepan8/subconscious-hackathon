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
  flex-direction: column;
  gap: 12px;
}
.strip__label { color: var(--text-faint); }
.strip__row {
  display: flex;
  align-items: center;
  gap: 32px;
  flex-wrap: wrap;
}
.strip__cell img {
  height: 28px;
  width: auto;
  opacity: 0.55;
  filter: grayscale(1) brightness(1.6) contrast(0.9);
  transition: opacity var(--dur-fast) var(--ease-out);
}
.strip__cell:hover img { opacity: 0.95; }
</style>
