<template>
  <div v-if="bookDetail">
    <BooksHeader>
      <template v-slot:left>
        <span @click="back()">back</span>
      </template>
      <h2>{{ title }}</h2>
      <template v-slot:right>
        <span v-if="!edit" @click="edit = true">edit</span>
      </template>
    </BooksHeader>
    <BooksFrom v-if="edit" v-model:data="bookDetail" :edit-flag="true" @back="back()"></BooksFrom>
    <BooksDetailInfo v-else :data="bookDetail"></BooksDetailInfo>
  </div>
</template>
<script setup lang="ts">
import type { booksInfo } from './index.vue';
const route = useRoute();
const router = useRouter();

const id = route.params.id;
const edit = ref(false);
const { data: bookDetail } = await useFetch<booksInfo>(`https://fe-interview-api.unnotech.com/books/${id}`);
const title = computed(() => bookDetail.value?.title);
function back() {
  if (edit.value) {
    edit.value = false;
  } else {
    router.back();
  }
}
</script>
