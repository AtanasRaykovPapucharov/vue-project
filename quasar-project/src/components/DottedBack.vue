<template>
  <div class="relative-position">
    <div class="absolute-right">
      <canvas class="bg-blue-9" ref="canvasRef" width="600" height="200" />
    </div>
    <div class="absolute-right text-white q-pa-lg" style="width: 50%">
      <p>
        The standard chunk of Lorem Ipsum used since the 1500s is reproduced
        below for those interested. Sections 1.10.32 and 1.10.33 from "de
        Finibus Bonorum et Malorum" by Cicero are also reproduced in their exact
        original form, accompanied by English versions from the 1914 translation
        by H. Rackham.
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, Ref, onMounted, onUnmounted } from 'vue';

const canvasRef: Ref<HTMLCanvasElement | undefined> = ref();
const context: Ref<CanvasRenderingContext2D | undefined> = ref();

const canvasRender = (steps = 1, stepSize = 4) => {
  let y = stepSize;
  if (canvasRef.value && context.value) {
    context.value.fillStyle = 'white';
    for (let i = stepSize * steps; i < canvasRef.value.width; i += stepSize) {
      if (y > canvasRef.value.height - stepSize)
        y = canvasRef.value.height - stepSize;
      for (let j = stepSize; j <= y; j += stepSize) {
        context.value.beginPath();
        context.value.arc(i, j, 0.5, 0, 2 * Math.PI, true);
        context.value.fill();
      }
      y += stepSize;
    }
  }
};

const canvasResize = () => {
  if (canvasRef.value) {
    canvasRef.value.width = window.innerWidth;
    canvasRender(window.innerWidth / 10);
  }
};

onMounted(() => {
  if (canvasRef.value) canvasRef.value.width = window.innerWidth;
  context.value = canvasRef.value?.getContext('2d') || undefined;
  canvasRender(window.innerWidth / 10);
  window.addEventListener('resize', canvasResize, false);
});

onUnmounted(() => {
  window.removeEventListener('resize', canvasResize, false);
});
</script>
