<template>
  <button class="button" :class="classObj">
    <BaseIcon v-if="hasIconLeft" :icon="computedIcon"/>
    <transition name="fade">
      <span class="button-text">
        <slot>
          {{ renderText }}
        </slot>
      </span>
    </transition>
    <BaseIcon v-if="hasIconRight" :icon="computedIcon"/>
  </button>
</template>

<script>
import BaseIcon from './BaseIcon.vue';

export default {
  name: 'BaseButton',
  props: {
    mod: {
      type: String,
      validator: (value) => ['primary', 'arrow', 'send'].includes(value),
      default: 'primary'
    },
    iconLeft: String,
    iconRight: String,
    sent: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    classObj() {
      return {
        [`button--${this.mod}`]: !!this.mod,
        "button--sent": !!this.mod && this.sent
      }
    },
    computedIcon() {
      return this.mod === 'arrow' ? 'arrow'
        : this.mod === 'send' ? 'send'
        : this.iconLeft ?? this.iconRight;
    },
    hasIconLeft() {
      return this.mod === 'arrow' ? false
        : this.mod === 'send' ? true
        : this.iconLeft;
    },
    hasIconRight() {
      return this.mod === 'arrow' ? true
        : this.mod === 'send' ? false
        : this.iconRight;
    },
    renderText() {
      if (this.mod === 'send' && this.sent) {
        return 'Ваше сообщение отправлено!'
      } else {
        return 'Отправить';
      }
    }
  },
  components: {
    BaseIcon
  }
}
</script>

<style lang="scss">
.button {
  $self: &;
  display: flex;
  cursor: pointer;
  border: none;
  position: relative;

  &-text {
    position: relative;
    z-index: 2;
  }

  &--arrow {
    background-color: transparent;
    color: get-var(color, blue_light);
    font-weight: 600;
    font-size: 16px;
    padding-right: 10px;
    gap: 10px;
    text-transform: uppercase;
    z-index: 2;

    &::after {
      content: '';
      @include create-figure(61px, transparent, 50%, 1px, get-var(color, grey_circle));
      position: absolute;
      right: 0;
      top: 50%;
      transform: translateY(calc(-50% - 2px));
      z-index: 1;
    }
  }

  &--send {
    $min-size: 216px;
    $max-size: 227px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    position: relative;
    @include create-figure(227px, transparent, 50%);
    width:  100%;
    height: 100%;

    @include to-responsive((
      min-width:  ($min-size, $max-size),
      max-width:  ($min-size, $max-size),
      min-height: ($min-size, $max-size),
      max-height: ($min-size, $max-size),
      font-size: (18px, 20px)
    ));
    border-radius: 50%;
    background: linear-gradient(93.29deg, #388AF3 21.04%, #A483E2 88.77%);
    transition: .25s;
    font-weight: 800;
    //font-size: 20px;
    //@include to-responsive(font-size, 18px, 20px);

    #{$self}-text {
      position: absolute;
      top: 65%;
      left: 50%;
      transform: translate(-50%, -50%);
      transition: .25s;
      color: #388AF3;
      width: 100%;
    }

    .icon {
      z-index: 1;
      position: absolute;
      top: 25%;
      right: 50%;
      transform: translateX(50%);
      transition: .25s;
      transform-origin: right top;
      @include to-responsive(font-size, 55px, 57px);
    }

    &::before {
      content: '';
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      @include create-figure(calc(100% - 19px), #FFF, 50%);
      // @include to-responsive((
      //   min-width:  ($min-size, $max-size),
      //   max-width:  ($min-size, $max-size),
      //   min-height: ($min-size, $max-size),
      //   max-height: ($min-size, $max-size),
      //   font-size: (18px, 20px)
      // ));
      transition: .25s;
    }

  }

  &--send:not(&--sent):hover, &--sent {
    background: linear-gradient(93.29deg, #388AF3 21.04%, #388AF3 88.77%);
    #{$self}-text {
      top: 50%;
      color: #FFF;
    }
    .icon {
      font-size: 96px;
      top: 5%;
      //right: 62px;
      right: 27%;
    }
    &::before {
      background-color: #388AF3;
    }
  }

  &--sent {
    .icon {
      font-size: 0px;
      top: 10%;
      right: 0%;
    }

    &, &::before, .icon, #{$self}-text {
      transition: 1s;
    }
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
}
</style>
