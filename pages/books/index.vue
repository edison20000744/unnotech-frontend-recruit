<template>
  <div class="container mx-auto px-4">
    <BooksHeader>
      <h2 class="font-bold text-3xl my-3">書本列表</h2>
      <template v-slot:right>
        <span @click="router.push('/books/add')">
          <font-awesome-icon icon="fa-solid fa-plus" />
        </span>
      </template>
    </BooksHeader>
    <div class="grid grid-cols-2 gap-2">
      <BooksCard
        class="hover:cursor-pointer"
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
  id?: number;
  image?: string;
}
</script>
