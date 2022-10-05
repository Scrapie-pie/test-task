<template>
  <div class="header-menu">
    <div class="header-menu-dot" />
    <div class="header-menu-dot" />
    <div class="header-menu-dot" />
  </div>
</template>

<script>
export default {
  name: 'HeaderMenu',
}
</script>

<style lang="scss">
.header-menu {
  @include flex-it(row, 5px);

  &-dot {
    $color: get-var(color, blue_light);
    @include create-figure(7px, $color, 50%);
  }

  @include media($min: sm) {
    position: fixed;
    left: 50px;
    top: 50%;
  }
}
</style>
