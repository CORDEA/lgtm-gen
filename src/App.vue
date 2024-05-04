<script setup lang="ts">
import DropArea from "./components/DropArea.vue";
import Preview from "./components/Preview.vue";
import DownloadButton from "./components/DownloadButton.vue";
import {ref} from "vue";
import Option from "./components/Option.vue";

const file = ref<File | null>(null)
const text = ref<string | null>('LGTM')
const color = ref<string | null>(null)
const size = ref<number | null>(40)
</script>

<template>
  <Preview :file="file" :text="text" :color="color" :size="size"/>
  <DropArea v-model:file="file"/>
  <Option v-if="file" v-model:text="text" v-model:color="color" v-model:size="size"/>
  <DownloadButton v-if="file"/>
</template>

<style scoped>
</style>
