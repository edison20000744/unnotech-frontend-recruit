<template>
  <div v-if="bookDetail">
    <BooksHeader>
      <template v-slot:left>
        <span @click="back()">
          <font-awesome-icon icon="fa-solid fa-chevron-left" />
        </span>
      </template>
      <h2 class="font-bold text-3xl my-3">{{ title }}</h2>
      <template v-slot:right>
        <span v-if="!edit" @click="edit = true">
          <font-awesome-icon icon="fa-solid fa-pen-to-square" />
        </span>
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
