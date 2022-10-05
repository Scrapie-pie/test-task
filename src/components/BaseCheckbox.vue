<template>
  <label class="checkbox">
    <input
      type="checkbox"
      @change="$emit('change', $event.target.checked)"
      v-bind="$attrs"
    >
    <span />
    <div class="checkbox-label">
      <slot/>
    </div>
  </label>
</template>

<script>
import BaseLabel from './BaseLabel.vue';

export default {
  name: "BaseCheckbox",
  inheritAttrs: false,
  model: {
    prop: 'checked',
    event: 'change'
  },
}
</script>

<style lang="scss">
.checkbox {
  @include flex-it(row, 20px);
  color: #D3D3D3;
  @include checker($el: span, $size: 30px, $indent: 0, $color: #388AF3);

  &-label {
    display: flex;
    align-items: center;
    white-space: pre;
  }
}

  // &[type="checkbox"] {
  //   $size: 16px;
  //   background-color: transparent;
  //   max-width:  $size;
  //   max-height: $size;
  //   min-width:  $size;
  //   min-height: $size;
  //   margin: 0;
  // }

</style>
