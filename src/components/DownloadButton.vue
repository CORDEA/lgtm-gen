<script setup lang="ts">
function onClick(_: MouseEvent) {
  const canvas = document.getElementById('canvas') as HTMLCanvasElement
  canvas.toBlob((blob) => {
    if (!blob) {
      return
    }
    const a = document.createElement('a')
    a.download = 'lgtm.png'
    a.href = URL.createObjectURL(blob)
    a.click()
  })
}
</script>

<template>
  <div class="card">
    <button @click="onClick" type="button" id="button">
      Export
    </button>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  margin-top: 64px;
}

button {
  margin: 0 0 0 auto;
  min-width: 120px;
  font-size: 1.2em;
  font-weight: 300;
  cursor: pointer;
  padding: 16px 32px;
  border: 1px solid #fafafa;
  background-color: transparent;
}

button:hover {
  background-color: #fafafa33;
}

@media (prefers-color-scheme: light) {
  button {
    border-color: #212121;
  }

  button:hover {
    background-color: #21212133;
  }
}

</style>
