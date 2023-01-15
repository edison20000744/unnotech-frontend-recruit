<template>
  <div class="book-card">
    <div class="title">{{ title }}</div>
    <div class="author">作者:{{ author }}</div>
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
  min-height: 20px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 10px;
  &:hover {
    box-shadow: 0 0 10px 1px #a1b300;
  }
  .title {
    font-size: 1.2rem;
    font-weight: bold;
    text-align: center;
  }
}
</style>
