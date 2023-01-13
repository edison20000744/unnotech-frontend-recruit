<template>
  <div class="book-detail">
    <div class="title">
      <label>名稱:{{ data.title }}</label>
    </div>
    <div class="author">
      <label>作者:{{ data.author }}</label>
    </div>
    <div class="description">
      <label>描述:{{ data.description }}</label>
    </div>
  </div>
</template>
<script setup lang="ts">
import type { booksInfo } from '../../pages/books/index.vue';
defineProps<{
  data: booksInfo;
}>();
</script>
<style lang="scss" scoped>
.book-detail {
  display: flex;
  flex-direction: column;
  footer {
    display: flex;
    justify-content: space-evenly;
  }
}
</style>
