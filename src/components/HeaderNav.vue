<template>
  <div class="header-nav">
    <span class="header-nav-item">Проекты</span>
    <span class="header-nav-item">О компании</span>
    <span class="header-nav-item active">Контакты</span>
  </div>
</template>

<script>

export default {
  name: 'HeaderNav',
  components: {
  }
}
</script>

<style lang="scss">
.header-nav {
  //@include flex-it(row, 50px);
  display: flex;
  @include to-responsive(gap, 15px, 50px);

  &-item {
    color: get-var(color, dark);
    font-weight: 600;

    &.active {
      color: get-var(color, blue_light);
      @include under-dot(7px);
    }
  }

  @include media($max: lg) {
    display: none;
  }
}
</style>
