<template>
  <div class="header d-flex space-between align-center gap-16">
    <h1 class="header-title">
      Добавление товара
    </h1>
    <div class="header__sort">
      <div class="select__container d-flex align-center">
        <select class="select" :value="modelValue" @change="updateModelValue($event.target.value)">
          <option v-for="(option, index) in optionList" :key="index" class="option" :label="option" :value="option"></option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TheHeader",
  props: {
    modelValue: {
      type: String,
      default: "По умолчанию"
    },
    optionList: {
      type: Array,
      required: true,
    },
  },
  emits: ['update:modelValue'],
  methods: {
    updateModelValue(newValue) {
      this.$emit('update:modelValue', newValue)
    }
  }
}
</script>

<style scoped lang="scss">
  .header {
    margin-bottom: 10px;
    &-title {
      font-weight: 600;
      font-size: 28px;
    }
  }
  .select {
    font-size: 12px;
    border: none;
    height: 100%;


    &__container {
      padding: 8px;
      background: $color-bg-main;
      box-shadow: 0 2px 5px #00000010;
    }
  }

  @media (max-width: 800px) {
    .header {
      flex-wrap: wrap;
    }
  }
  @media (max-width: 800px) {
    .header {
      flex-wrap: wrap;
    }
  }
  @media (max-width: 576px) {
    .header {
      flex-wrap: wrap;
      justify-content: center !important;
    }
  }
</style>
