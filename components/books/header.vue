<template>
  <header>
    <div class="left">
      <slot name="left"></slot>
    </div>
    <div class="center">
      <slot></slot>
    </div>
    <div class="right">
      <slot name="right"></slot>
    </div>
  </header>
</template>
<style lang="scss" scoped>
header {
  display: grid;
  grid-template-columns: 50px 1fr 50px;
  justify-items: center;
  align-items: center;
}
</style>
