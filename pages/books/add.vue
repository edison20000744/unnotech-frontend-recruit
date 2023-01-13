<template>
  <div>
    <BooksHeader>
      <template v-slot:left>
        <span @click="router.back()">back</span>
      </template>
      <h2>新增書本</h2>
    </BooksHeader>
    <BooksFrom action="add"></BooksFrom>
  </div>
</template>
<script setup lang="ts">
const router = useRouter();
</script>
