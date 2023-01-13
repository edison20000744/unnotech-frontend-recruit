<template>
  <div class="book-detail">
    <div class="title">
      <label>名稱:</label>
      <input v-model="formData.title" />
    </div>
    <div class="author">
      <label>作者:</label>
      <input v-model="formData.author" />
    </div>
    <div class="description">
      <label>描述:</label>
      <textarea v-model="formData.description"></textarea>
    </div>
    <footer>
      <button>取消</button>
      <button @click="actionHandle()">{{ action === 'edit' ? '修改' : '新增' }}</button>
    </footer>
  </div>
</template>
<script setup lang="ts">
import type { booksInfo } from '../../pages/books/index.vue';
const props = defineProps<{
  data?: booksInfo;
  action: 'add' | 'edit';
}>();
const formData = computed(() => props.data || { title: '', author: '', description: '' });

function actionHandle() {
  if (props.action === 'add') {
    add();
  }
  if (props.action === 'edit' && props.data?.id) {
    edit(props.data.id);
  }
}
async function add() {
  const { data } = await useFetch<booksInfo>(`https://fe-interview-api.unnotech.com/books/`, {
    method: 'POST',
    body: formData.value,
  });
}
async function edit(id: number) {
  const { data } = await useFetch<booksInfo>(`https://fe-interview-api.unnotech.com/books/${id}`, {
    method: 'PATCH',
    body: formData.value,
  });
}
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
