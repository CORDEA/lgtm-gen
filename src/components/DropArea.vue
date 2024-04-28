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
  <div class="card" @dragover="onDrag" @drop="onDrop">
    <p>Drop the image</p>
  </div>
</template>

<style scoped>

.card {
  width: 80vw;
  padding: 64px;
  background: #ffffffa0;
  border-radius: 24px;
  border: #ffffff dashed 1px;
}

</style>
