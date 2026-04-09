<!--
  DotGrid — background grid used on hero / section slides.
-->
<template>
  <div class="dotgrid" aria-hidden="true">
    <div class="dotgrid__fade"></div>
  </div>
</template>

<style scoped>
.dotgrid {
  position: absolute;
  inset: 0;
  background-image: radial-gradient(circle at 1px 1px, rgba(255,255,255,0.08) 1px, transparent 0);
  background-size: 36px 36px;
  mask-image: radial-gradient(ellipse at center, black 40%, transparent 78%);
  -webkit-mask-image: radial-gradient(ellipse at center, black 40%, transparent 78%);
  pointer-events: none;
}
.dotgrid__fade {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 50% 65%, rgba(255, 92, 40, 0.12), transparent 55%);
}
</style>
