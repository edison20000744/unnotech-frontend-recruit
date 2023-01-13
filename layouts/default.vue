<template>
  <Suspense :timeout="0">
    <template #default>
      <slot />
    </template>
    <template #fallback>
      <div>loadding</div>
    </template>
  </Suspense>
</template>
<script setup lang="ts"></script>
<style lang="scss" scoped></style>
