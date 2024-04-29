<script setup lang="ts">
import {watch} from "vue";

const props = defineProps(['file'])

watch(props, async (next, _) => {
  const canvas = document.getElementById('canvas') as HTMLCanvasElement
  const ctx = canvas.getContext('2d');
  if (!ctx) {
    return;
  }
  const reader = new FileReader();
  const img = new Image();
  img.onload = () => {
    canvas.width = img.width
    canvas.height = img.height
    ctx.drawImage(img, 0, 0)
  }
  reader.onload = (e) => {
    img.src = e.target?.result as string
  }
  reader.readAsDataURL(next.file);
})
</script>

<template>
  <canvas id="canvas" width="0" height="0"></canvas>
</template>

<style scoped>
</style>
