<script setup lang="ts">
const file = defineModel('file')

function hasImage(data: DataTransfer | null): boolean {
  const items = data?.items ?? []
  if (items.length <= 0) {
    return false
  }
  const item = items[0]
  if (item.kind !== 'file') {
    return false
  }
  return item.type.startsWith('image');
}

function onDrag(event: DragEvent) {
  if (hasImage(event.dataTransfer)) {
    event.preventDefault()
  }
}

function onDrop(event: DragEvent) {
  const data = event.dataTransfer
  if (!hasImage(data)) {
    return
  }
  event.preventDefault()
  const item = data!.items[0]
  file.value = item.getAsFile()
}
</script>

<template>
  <div class="card" @dragover="onDrag" @drop="onDrop" v-if="!file">
    <p>Drop the image</p>
  </div>
  <div class="mini-card" @dragover="onDrag" @drop="onDrop" v-else>
    <p>Or drop the image</p>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  width: 80vw;
  height: 20vh;
  padding: 64px;
  border: 5px solid;
  border-image: linear-gradient(
      0deg,
      #fafafa 20%,
      transparent 20% 80%,
      #fafafa 80%
  ) 1;
  border-image: -webkit-linear-gradient(
      0deg,
      #fafafa 20%,
      transparent 20% 80%,
      #fafafa 80%
  ) 1;
}

.mini-card {
  display: flex;
  width: 80vw;
  padding: 32px;
  margin: 64px 0;
  border: 2px solid;
  border-image: linear-gradient(
      0deg,
      #fafafa 20%,
      transparent 20% 80%,
      #fafafa 80%
  ) 1;
  border-image: -webkit-linear-gradient(
      0deg,
      #fafafa 20%,
      transparent 20% 80%,
      #fafafa 80%
  ) 1;
}

.card > p {
  margin: auto;
  font-size: 2em;
  font-weight: bold;
}

.mini-card > p {
  margin: auto;
  font-size: 1em;
}

@media (prefers-color-scheme: light) {
  .card {
    border-image: linear-gradient(
        0deg,
        #212121 20%,
        transparent 20% 80%,
        #212121 80%
    ) 1;
    border-image: -webkit-linear-gradient(
        0deg,
        #212121 20%,
        transparent 20% 80%,
        #212121 80%
    ) 1;
  }

  .mini-card {
    border-image: linear-gradient(
        0deg,
        #212121 20%,
        transparent 20% 80%,
        #212121 80%
    ) 1;
    border-image: -webkit-linear-gradient(
        0deg,
        #212121 20%,
        transparent 20% 80%,
        #212121 80%
    ) 1;
  }
}
</style>
