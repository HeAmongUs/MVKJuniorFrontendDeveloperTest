<template>
    <aside class="sidebar d-flex flex-column gap-16">
      <div class="sidebar__item">
        <div class="sidebar__item-title required">Наименование товара</div>
        <div class="sidebar__item__input">
          <input
            v-model="newProduct.title"
            type="text"
            placeholder="Введите наименование товара"
            :class="{'error-field': newProduct.title !== null && !isValidTitle}"
            class="sidebar__item__input-input" />
          <div class="bar"></div>
          <small
            v-if="newProduct.title !== null && !isValidTitle"
            class="error-message">
            {{ errorMessageIsRequiredField }}
          </small>
        </div>
      </div>
      <div class="sidebar__item">
        <div class="sidebar__item-title">Описание товара</div>
        <div class="sidebar__item__input">
          <textarea
            v-model="newProduct.description"
            placeholder="Введите описание товара"
            class="sidebar__item__input-textarea" />
          <div class="bar"></div>
        </div>
      </div>
      <div class="sidebar__item">
        <div class="sidebar__item-title required">Ссылка на изображение товара</div>
        <div class="sidebar__item__input">
          <input
            v-model="newProduct.imgLink"
            type="text"
            placeholder="Введите ссылку"
            :class="{'error-field': newProduct.imgLink !== null && !isValidImgLink}"
            class="sidebar__item__input-input" />
          <div class="bar"></div>
          <small
            v-if="newProduct.imgLink !== null && !isValidImgLink"
            class="error-message">
            {{ errorMessageIsRequiredField }}
          </small>
        </div>
      </div>
      <div class="sidebar__item">
        <div class="sidebar__item-title required">Цена товара</div>
        <div class="sidebar__item__input">
          <input
            v-model.lazy="newProduct.cost"
            type="text"
            placeholder="Введите цену"
            class="sidebar__item__input-input"
            :class="{'error-field': newProduct.cost !== null && !isValidCost}"
            @input="updateCost($event.target.value)" />
          <div class="bar"></div>
          <small
            v-if="newProduct.cost !== null && !isValidCost"
            class="error-message">
            {{ errorMessageIsRequiredField }}
          </small>
        </div>
      </div>
      <input
        type="button"
        :disabled="!isValidForm"
        value="Добавить товар"
        class="sidebar-submit"
        @click="addNewProduct">
    </aside>
</template>

<script>
export default {
  name: 'TheSidebar',
  emits: ["add-new-product"],
  data() {
    return {
      newProduct: {
        title: null,
        description: null,
        cost: null,
        imgLink: null,
      },
      isShowError: false,
      errorMessageIsRequiredField: "Это обязательное поле",
    }
  },
  computed: {
    isValidForm() {
      return this.isValidTitle && this.isValidImgLink && this.isValidCost
    },
    isValidTitle() {
      return !!this.newProduct.title
    },
    isValidImgLink() {
      return !!this.newProduct.imgLink
    },
    isValidCost() {
      return !!this.newProduct.cost
    },
  },
  methods: {
    updateCost(newValue) {
      this.newProduct.cost = Number(newValue).toFixed(2)
    },
    addNewProduct() {
      this.$emit('add-new-product', this.newProduct)
      this.newProduct = {
        title: null,
        description: null,
        cost: null,
        imgLink: null,
      }
    },
  }
}
</script>

<style scoped lang="scss">
  .sidebar{
    padding: 24px;
    background: $color-bg-main;
    width: 332px;
    flex-shrink: 0;
    flex-grow: 0;
    max-height: 440px;
    border-radius: 4px;
    box-shadow: 0 0 20px #00000030, 2px 2px 10px #00000010;

    &__item {
      position: relative;

      .error-message {
        font-size: 8px;
        position: absolute;
        bottom: -12px;
        left: 0;
        color: $color-red;
      }
      .error-field {
        border: 1px solid $color-red !important;
      }
      .error-field + .bar {
        opacity: 0 !important;
      }
      .bar {
        position: absolute;
        bottom: 0;
        width: 0;
        height: 1px;
        background: $color-green;
        transition: all 0.5s;
        opacity: 0;
      }
      &-title {
        width: fit-content;
        font-size: 10px;
        margin-bottom: 4px;
        color: $color-sidebar-title;
      }
      &__input {
        max-height: 108px;
        &:hover {
          .bar {
            opacity: 1;
            width: 100%;
          }
        }
        &-input, &-textarea {
          box-shadow: 0 2px 5px #00000010;
          padding: 10px 16px;
          &:focus {
            border-bottom: 1px solid $color-green;
          }
        }
        &-textarea {
          box-sizing: border-box;
          font-size: 12px;
          width: 100%;
          max-height: 108px;
          min-height: 108px;

          &::placeholder{
            color: $color-sidebar-input-placeholder;
          }
        }
        &-input {
          font-size: 12px;
          width: 100%;
          height: 36px;
          transition: 0.3s;
          border: 1px solid transparent;

          &::placeholder{
            color: $color-sidebar-input-placeholder;
          }
        }
      }
    }

    &-submit {
      position: relative;
      margin-top: 8px;
      padding: 10px;
      width: 100%;
      cursor: pointer;
      background: $color-green;
      color: white;
      border-radius: 10px;
      font-size: 12px;
      font-weight: 600;
      transition: 0.3s;

      &:hover {
        transform: translateY(-2px);
        box-shadow: 2px 2px 8px $color-green, 0 -1px 4px $color-green,;
      }
    }
  }

  .required {
    position: relative;

    &::after {
      position: absolute;
      content: "";
      background: $color-red;
      top: -2px;
      right: -4px;
      width: 4px;
      height: 4px;
      border-radius: 50%;
    }
  }

  input[disabled][type="button"] {
    background: $color-sidebar-button-disabled;
    box-shadow: none;
    color: $color-sidebar-input-placeholder;
    &:hover {
      transform: none;
    }
  }

  @media (min-width: 1401px) {
    .sidebar{
      width: 350px;
      max-height: 455px;
      &__item {
        &-title {
          font-size: 14px;
        }
        &-textarea {
          font-size: 16px;
        }
        &-input {
          font-size: 16px;
        }
      }
      &-submit {
        font-size: 14px;
      }
    }

    .required {
      position: relative;

      &::after {
        position: absolute;
        content: "";
        background: $color-red;
        top: 0;
        right: -5px;
        width: 4px;
        height: 4px;
        border-radius: 50%;
      }
    }
  }

  @media (max-width: 576px) {
    .sidebar {
      width: 100%;
    }
  }

</style>
