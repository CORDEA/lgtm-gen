<script setup lang="ts">
const text = defineModel('text')
const color = defineModel('color')
const size = defineModel('size')
</script>

<template>
  <div class='card'>
    <input type='text' id='text' placeholder="Text" v-model="text"/>
    <input type='color' id='color' v-model="color"/>
    <input type='range' id='size' v-model="size"/>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
}

#text {
  border: 1px solid #fafafa;
  padding: 12px 16px;
}

#color {
  border: 1px solid #fafafa;
  margin: 16px 0 0 auto;
}

#size {
  margin-top: 16px;
  accent-color: #fafafa;
}

@media (prefers-color-scheme: light) {
  #text {
    border-color: #212121;
  }

  #color {
    border-color: #212121;
  }

  #size {
    accent-color: #212121;
  }
}
</style>
