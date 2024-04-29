<script setup lang="ts">
import DropArea from "./components/DropArea.vue";
import Preview from "./components/Preview.vue";
import DownloadButton from "./components/DownloadButton.vue";
import {ref} from "vue";

const file = ref<File | null>(null)
</script>

<template>
  <Preview :file="file"/>
  <DropArea v-model:file="file"/>
  <DownloadButton v-if="file"/>
</template>

<style scoped>
</style>
