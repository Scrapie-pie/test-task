<template>
  <div class="header-languages">
    <span class="header-languages-item active">RU</span>
    <span class="header-languages-item">EN</span>
  </div>
</template>

<script>

export default {
  name: 'HeaderLanguages',
  components: {
  }
}
</script>

<style lang="scss">
.header-languages {
  @include flex-it(row, 15px);

  &-item {
    font-size: 16px;
    color: get-var(color, grey);
    font-weight: 600;

    &.active {
      color: get-var(color, blue_light);
      @include under-dot(4px);
    }
  }
}
</style>
