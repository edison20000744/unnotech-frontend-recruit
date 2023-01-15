<template>
  <div class="book-card flex flex-col gap-4 border p-4 hover:shadow-xl hover:shadow-cyan-500/50">
    <div class="title text-1xl text-center font-bold text-gray-500 truncate">{{ title }}</div>
    <div class="author">作者:{{ author }}</div>
    <div class="description text-blue-300">{{ description }}</div>
  </div>
</template>
<script setup lang="ts">
const props = defineProps<{
  title: string;
  author: string;
  description: string;
}>();
</script>

<style lang="scss" scoped>
.book-card {
  min-height: 100px;
}
</style>
