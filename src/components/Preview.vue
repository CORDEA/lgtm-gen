<script setup lang="ts">
import { watch } from "vue";

const props = defineProps(["file", "text", "color", "size"]);

watch(props, async (next, _) => {
  const canvas = document.getElementById("canvas") as HTMLCanvasElement;
  const ctx = canvas.getContext("2d");
  if (!ctx) {
    return;
  }
  const font = getComputedStyle(canvas, null).getPropertyValue("font-family");
  const reader = new FileReader();
  const img = new Image();
  const width = parseFloat(
    getComputedStyle(canvas, null).getPropertyValue("width"),
  );
  img.onload = () => {
    const ar = img.height / img.width;
    canvas.width = width;
    canvas.height = width * ar;
    ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
    ctx.font = `${props.size}px ${font}`;
    ctx.fillStyle = props.color;
    ctx.textAlign = "center";
    ctx.textBaseline = "middle";
    ctx.fillText(props.text, canvas.width / 2, canvas.height / 2, canvas.width);
  };
  reader.onload = (e) => {
    img.src = e.target?.result as string;
  };
  reader.readAsDataURL(next.file);
});
</script>

<template>
  <canvas id="canvas" width="0" height="0"></canvas>
</template>

<style scoped>
#canvas {
  width: 60vw;
}
</style>
