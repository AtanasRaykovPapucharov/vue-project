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
import { ref, Ref, onMounted } from 'vue';

const canvasRef: Ref<HTMLCanvasElement | undefined> = ref();
const context: Ref<CanvasRenderingContext2D | undefined> = ref();
const canvasRender = () => {
  if (canvasRef.value && context.value) {
    const STEP = 4;
    context.value.fillStyle = 'white';
    for (let i = STEP; i < canvasRef.value.width; i += STEP) {
      for (let j = STEP; j <= i; j += STEP) {
        context.value.beginPath();
        context.value.arc(i, j, 0.5, 0, 2 * Math.PI, true);
        context.value.fill();
      }
    }
  }
};

onMounted(() => {
  context.value = canvasRef.value?.getContext('2d') || undefined;
  canvasRender();
});
</script>
