<template>
  <div class="book-card">
    <div class="title">{{ title }}</div>
    <div class="author">{{ author }}</div>
    <div class="description">{{ description }}</div>
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
  border: 1px solid black;
}
</style>
