<template>
  <header class="header">
    <BaseIcon icon="logo" class="header-logo"/>
    <HeaderNav/>
    <div class="header-side">
      <HeaderLanguages/>
      <BaseButton mod="arrow">Начать проект</BaseButton>
    </div>
    <HeaderMenu />
  </header>
</template>

<script>
import BaseIcon from './BaseIcon.vue';
import BaseButton from './BaseButton.vue';
import HeaderNav from './HeaderNav.vue';
import HeaderLanguages from './HeaderLanguages.vue';
import HeaderMenu from './HeaderMenu.vue';

export default {
  name: 'TheHeader',
  components: {
    BaseButton,
    BaseIcon,
    HeaderNav,
    HeaderLanguages,
    HeaderMenu
  }
}
</script>

<style lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 30px;
  width: 100%;
  @include container(1820px);

  @include to-responsive((
    padding-top: (30px, 60px),
    margin-bottom: (60px, 140px)
  ));

  &-side {
    @include flex-it(row, 10px);
    justify-content: space-between;
    align-items: center;
  }

  &-logo {
    @include to-responsive(font-size, 84px, 112px);
  }

  @include media($min: sm) {
    display: grid;
    grid-template-columns: 280px auto 280px;
  }

  @include media($max: lg) {
    grid-template-columns: 1fr 280px;
  }

  @include media($max: sm) {
    &-side {
      display: none;
    }
  }
}
</style>
