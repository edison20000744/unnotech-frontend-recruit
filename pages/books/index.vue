<template>
  <div class="book-container">
    <BooksHeader>
      <h2>書本列表</h2>
      <template v-slot:right>
        <span @click="router.push('/books/add')">add</span>
      </template>
    </BooksHeader>
    <div class="book-list">
      <BooksCard
        v-for="(item, index) in bookList"
        :key="index"
        :title="item.title"
        :author="item.author"
        :description="item.description"
        @click="router.push(`/books/${item.id}`)"
      ></BooksCard>
    </div>
  </div>
</template>
<script setup lang="ts">
const router = useRouter();
const { data: bookList } = await useFetch<booksInfo[]>('https://fe-interview-api.unnotech.com/books/');
</script>
<script lang="ts">
export interface booksInfo {
  title: string;
  author: string;
  description: string;
  id: number;
  image: string;
  v?: string;
  w?: string;
  h?: string;
}
</script>
<style lang="scss" scoped>
.book-container {
  .book-list {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
  }
}
</style>
