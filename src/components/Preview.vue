<script setup lang="ts">
import {ref, watch} from "vue";

const props = defineProps(['file'])
const file = ref<string | null>(null)

watch(props, async (next, _) => {
  const reader = new FileReader();
  reader.onload = (e) => {
    file.value = e.target?.result as string
  };
  reader.readAsDataURL(next.file);
})

</script>

<template>
  <img :src="file" alt="Preview" v-if="file"/>
</template>

<style scoped>
img {
  width: 80vw;
  padding: 64px;
}
</style>
