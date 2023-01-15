<template>
  <div class="container mx-auto px-20 min-w-full">
    <BooksHeader>
      <template v-slot:left>
        <span @click="router.back()">back</span>
      </template>
      <h2 class="font-bold text-3xl my-3">新增書本</h2>
    </BooksHeader>
    <BooksFrom v-model:data="fromData"></BooksFrom>
  </div>
</template>
<script setup lang="ts">
const router = useRouter();
const fromData = ref({ title: '', author: '', description: '' });
</script>
