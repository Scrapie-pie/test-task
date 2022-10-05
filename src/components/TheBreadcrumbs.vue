<template>
  <div class="breadcrumbs breadcrumbs--container">
    <span class="breadcrumbs-item">Главная</span>
    <span class="breadcrumbs-item">Контакты</span>
  </div>
</template>

<script>

export default {
  name: 'TheBreadcrumbs',
}
</script>

<style lang="scss">
.breadcrumbs {
  margin-bottom: 60px;

  &-item {
    @include h(6, get-var(color, graphit));

    &:not(:last-child):after {
      content: '\00a0-\00a0';
    }

    &:last-child {
      font-weight: 600;
    }
  }
}
</style>
