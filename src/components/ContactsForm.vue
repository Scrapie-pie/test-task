<template>
  <form class="contacts-form contacts-form--container" @submit.prevent="sendForm">
    <h1>Мы рядом</h1>
    <h5>
      Заполните форму ниже и мы свяжемся с вами. Не любите формы?
      Напишите нам на почту <BaseContact type="mail" value="info@site.com"/>
    </h5>

    <div class="contacts-form-wrapper">
      <div>
        <div class="contacts-form-fields">
          <BaseField v-model="inputs.name" type="text" placeholder="Ваше Имя" required />
          <BaseField v-model="inputs.mail" type="mail" placeholder="Ваш E-Mail" required />
          <BaseField v-model="inputs.comment" type="textarea" placeholder="Комментарий" required />
        </div>

        <BaseCheckbox v-model="inputs.okPolite">Согласен с <BaseLink>Политикой конфиденциальности</BaseLink></BaseCheckbox>
      </div>

      <BaseButton type="submit" mod="send" :sent="isFormSent"></BaseButton>
    </div>



  </form>
</template>

<script>
import BaseInput from './BaseInput.vue';
import BaseButton from './BaseButton.vue';
import BaseField from './BaseField.vue';
import BaseContact from './BaseContact.vue';
import BaseLink from './BaseLink.vue';
import BaseCheckbox from './BaseCheckbox.vue';
export default {
  name: 'ContactsForm',
  data() {
    return {
      isFormSent: false,
      inputs: {
        name: '',
        mail: '',
        comment: '',
        okPolite: false,
      }
    }
	},
	methods: {
    sendForm() {
      if (this.inputs.okPolite) {
        this.isFormSent = true;
      }
    }
	},
  components: {
    BaseInput,
    BaseButton,
    BaseField,
    BaseContact,
    BaseLink,
    BaseCheckbox
  }
}
</script>

<style lang="scss">
.contacts-form {
  &-wrapper {
    @include flex-it(row, 30px);
    justify-content: space-between;

    @include to-responsive(padding-top, 80px, 120px);
  }

  &-wrapper {
    display: flex;
  }

  &-fields {
    display: grid;
    grid-template-columns: minmax(150px, 430px) minmax(150px, 280px);
    padding-bottom: 30px;
    column-gap: 30px;
    row-gap: 60px;

    & > *:nth-child(3) {
      grid-column: 1/-1;
    }
  }

  @include media($min: lg) {
    &-wrapper {
      align-items: flex-end;
    }
  }

  @include media($max: lg) {
    &-wrapper {
      flex-direction: column;
    }
  }
}
</style>
