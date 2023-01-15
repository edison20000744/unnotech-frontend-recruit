<template>
  <div class="book-detail">
    <VForm :validation-schema="schema" :initial-values="initialValues" v-slot="{ meta: formMeta, resetForm }" @submit="actionHandle">
      <div class="title">
        <VTextInput name="title" label="名稱" placeholder="名稱" />
      </div>
      <div class="author">
        <VTextInput name="author" label="作者" placeholder="作者" />
      </div>
      <div class="description">
        <label>描述:</label>
        <VField as="textarea" name="description" rows="15" maxlength="400" class="border border-black"></VField>
      </div>
      <footer class="flex justify-evenly">
        <button type="button" class="bg-gray-400 px-5 py-2.5 text-sm leading-5 rounded-md font-semibold text-white" @click="resetForm()">取消</button>
        <button
          class="bg-sky-500 hover:bg-sky-700 px-5 py-2.5 text-sm leading-5 rounded-md font-semibold text-white"
          :class="{ 'is-primary': formMeta.valid }"
          :disabled="!formMeta.valid || sending"
          type="submit"
        >
          {{ sending ? 'sending...' : editFlag ? '修改' : '新增' }}
        </button>
        <!-- <span @click="del()">刪除</span> -->
      </footer>
    </VForm>
  </div>
</template>
<script setup lang="ts">
import { object, string } from 'yup';
import { configure } from 'vee-validate';
import type { SubmissionContext } from 'vee-validate';
import type { booksInfo } from '../../pages/books/index.vue';

const props = withDefaults(
  defineProps<{
    data: booksInfo;
    editFlag?: boolean;
  }>(),
  {
    editFlag: false,
  }
);
const emit = defineEmits({
  'update:data': (payload: booksInfo) => true,
  back: () => true,
});
const router = useRouter();
const BOOK_URL = 'https://fe-interview-api.unnotech.com/books';
const initialValues = { ...props.data };
const formData = ref({ ...props.data });
const sending = ref(false);

configure({
  validateOnBlur: true, // controls if `blur` events should trigger validation with `handleChange` handler
  validateOnChange: true, // controls if `change` events should trigger validation with `handleChange` handler
  validateOnInput: false, // controls if `input` events should trigger validation with `handleChange` handler
  validateOnModelUpdate: true, // controls if `update:modelValue` events should trigger validation with `handleChange` handler
});
const schema = object({
  title: string().required().label('名稱'),
  author: string().required().label('作者'),
  description: string(),
});

function actionHandle(values: booksInfo, actions: SubmissionContext) {
  formData.value = values;
  sending.value = true;
  if (props.editFlag && props.data?.id) {
    edit(props.data.id);
  } else {
    add();
  }
}
async function add() {
  await useFetch<booksInfo>(`${BOOK_URL}`, {
    method: 'POST',
    body: formData.value,
  }).then(({ data }) => {
    sending.value = false;
    router.push(`/books/${data.value?.id}`);
  });
}
async function edit(id: number) {
  await useFetch<booksInfo>(`${BOOK_URL}/${id}`, {
    method: 'PATCH',
    body: formData.value,
  })
    .then(({ data }) => {
      sending.value = false;
      if (data.value) emit('update:data', data.value);
      emit('back');
    })
    .catch();
}

async function del() {
  if (props.data?.id) {
    await useFetch<booksInfo>(`${BOOK_URL}/${props.data.id}`, {
      method: 'DELETE',
    })
      .then(() => router.push('/books'))
      .catch();
  }
}
</script>
<style lang="scss" scoped>
@import './assets/book-detail.scss';
</style>
