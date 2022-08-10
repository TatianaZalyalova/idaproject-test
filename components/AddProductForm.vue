<template>
  <div class="wrapper">
    <h2 class="header">Добавление товара</h2>
    <form class="form" @submit="createProductObj">
      <p class="form__wrap">
        <label for="name" class="form__label label">
            <span class="label__wrap label__wrap_required">
                Наименование товара
            </span>
        </label>
        <input
          id="title"
          v-model="title"
          type="text"
          class="form__input"
          placeholder="Введите наименование товара"
           required
          @input="enableButton"
        />
      </p>
      <p class="form__wrap">
        <label for="description" class="form__label label">
            <span class="label__wrap">Описание товара</span>
        </label>
        <textarea
          id="description"
          v-model="description"
          type="text"
          placeholder="Введите описание товара"
          class="form__textarea"></textarea>
      </p>
      <p class="form__wrap">
        <label for="img" class="form__label label">
            <span class="label__wrap label__wrap_required">
                Ссылка на изображение товара</span>
            </label>
        <input
          id="img"
          v-model="img"
          type="text"
          class="form__input"
          placeholder="Введите ссылку"
          required
          @input="enableButton"
        />
      </p>
      <p class="form__wrap">
        <label for="price" class="form__label label">
            <span class="label__wrap label__wrap_required">
                Цена товара</span>
            </label>
        <input
          id="price"
          v-model="price"
          type="text"
          class="form__input"
          placeholder="Введите цену"
          required
          @input="enableButton"
          oninput="this.value = this.value.replace(/[^0-9]/g, '')"
        />
      </p>
      <button class="form__button" :disabled="isDisabled">
        Добавить товар
      </button>
    </form>
  </div>
</template>
<script>
export default {
  name: 'AddProductForm',
  props: {
    addProduct: Function,
  },
  data() {
    return {
      title: '',
      description: '',
      img: '',
      price: '',
      isDisabled: true,
    }
  },

  methods: {
    createProductObj(event) {
      event.preventDefault()

      this.addProduct({
        id: this.createId(),
        title: this.title,
        description: this.description,
        img: this.img,
        price: this.price,
      })
      this.title = ''
      this.description = ''
      this.img = ''
      this.price = ''
      this.enableButton()
    },
    createId() {
      return Math.random().toString(16).slice(2)
    },
    enableButton() {
      this.isDisabled = !(this.title && this.img && this.price)
    },
  },
}
</script>
<style lang="scss" scoped>
@mixin input {
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  width: 284px;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #3f3f3f;
  padding: 11px 16px 10px;
  border: none;
  outline: none;

  &::-webkit-input-placeholder {
    color: #b4b4b4;
  }

  &:-moz-placeholder {
    color: #b4b4b4;
  }

  &:hover {
    box-shadow: 0 0 4px rgba(0, 0, 0, 0.5);
  }

  &:focus {
    box-shadow: 0 0 4px rgb(94, 90, 90);
  }
}
.form {
  width: 332px;
  background: #fffefb;
  border-radius: 4px;
  padding: 24px;
  box-shadow: 0px 20px 30px rgba(0 0 0 /4%), 0px 6px 10px rgba(0 0 0 /2%);
  margin-right: 16px;

  .form__wrap {
    margin-bottom: 0;
    margin-top: 0;

    & + .form__wrap {
      margin-top: 16px;
    }
  }
  .form__label {
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: #49485e;
    display: block;
    margin-bottom: 4px;

    .label__wrap_required {
      position: relative;
      &:after {
        content: '';
        display: block;
        width: 4px;
        height: 4px;
        background: #ff8484;
        border-radius: 4px;
        position: absolute;
        top: 0;
        right: -5px;
      }
    }
  }

  .form__input {
    @include input;
  }

  .form__textarea {
    @include input;
    resize: none;
    height: 104px;
  }

  .form__button {
    background: #7bae73;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    width: 284px;
    letter-spacing: -0.02em;
    color: #ffffff;
    font-weight: 600;
    font-size: 12px;
    line-height: 15px;
    padding-top: 10px;
    padding-bottom: 11px;
    font-family: 'Inter';
    display: inline-block;
    text-align: center;
    margin-top: 24px;
    border: none;

    &:disabled {
      background-color: #eeeeee;
      color: #b4b4b4;
      box-shadow: none;
    }
  }
}

@media (max-width: 1024px) {
  .form {
    margin-right: auto;
    margin-left: auto;
    margin-bottom: 30px;
  }
}
</style>
