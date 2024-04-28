<script setup lang="ts">
import DropArea from "./components/DropArea.vue";
import Preview from "./components/Preview.vue";
import {ref} from "vue";

const file = ref<File | null>(null)
</script>

<template>
  <Preview :file="file"/>
  <DropArea v-model:file="file"/>
</template>

<style scoped>
</style>
