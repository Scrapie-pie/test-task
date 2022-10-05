<template>
  <label class="field" :class="[activeClass, `field__${type}`]">
    <span v-if="label" class="field__name">
      {{label}}
    </span>
    <div :class="`field__wrapper`">

      <div class="field__action">
        <div class="field__fit">
          <BaseTextarea
            v-if="type === 'textarea'"
            v-bind="$attrs"
            @input="$emit('input', $event)"
          />
          <BaseInput
            v-else
            v-bind="$attrs"
            :type="type"
            @input="passValue"
          />
          <span
            v-if="placeholder"
            class="field__placeholder"
          >
            {{placeholder}}
          </span>
        </div>
      </div>
    </div>
  </label>
</template>

<script>
import BaseInput from './BaseInput.vue';
import BaseTextarea from './BaseTextarea.vue';

export default {
  name: 'BaseField',
  inheritAttrs: false,
  props: {
    type: {
      type: String,
      default: 'text',
    },
    label: String,
    placeholder: String,
    options: Array,
  },
  data() {
    return {
      activeClass: null,
    }
  },
  methods: {
    passValue(value) {
      this.activeClass = value.length ? 'not-empty' : null;
      this.$emit('input', value);
    }
  },
  components: {
    BaseInput,
    BaseTextarea
  }
}
</script>

<style lang="scss">
//background: #CCCCCC;

.field {
  $field: &;

  width: 100%;
  @include flex-it(column, 10px);

  &__name {
    color: get-var(color, grey_dark);
    width: min-content;
  }

  #{$field}__action {
    position: relative;
    display: flex;
    align-items: center;
    padding-bottom: 4px;
    width: 100%;


    @include h(3, $color: #343434, $weight: 300);

    font-size: 26px;
    font-weight: 300;
    border-bottom: 1px solid #E2E2E2;
  }

  #{$field}__fit {
    width: 100%;
    position: relative;
  }

  #{$field}__placeholder {
    position: absolute;
    width: 100%;
    left: 0;
    pointer-events: none;
    @include h(3, $color: #CCCCCC, $weight: 300);
    //color: #CCCCCC;
    transition: .25s ease-out;
  }

  &__text, &__password, &__mail {
    #{$field}__placeholder {
      top: 50%;
      transform: translateY(-50%);
    }
  }

  .input, .textarea {
    width: 100%;
    font-weight: 300;

    &[required] + #{$field}__placeholder {
      &:after {
        content: ' *';
        color: #FF1300;
      }
    }
  }

  .input:focus + #{$field}__placeholder {
    font-size: 16px;
    top: -10px;
    transition: .1s ease-in;
  }

  &__textarea {
    padding-top: 60px;
    .textarea {
      height: 1em;
      overflow: hidden;
    }

    #{$field}__placeholder {
      bottom: 60px;
    }
  }

  &.not-empty {
    .input + #{$field}__placeholder {
      font-size: 16px;
      top: -10px;
      transition: .1s ease-in;
    }
  }
}
</style>
