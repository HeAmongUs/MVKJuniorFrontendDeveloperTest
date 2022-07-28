<template>
  <div class="header d-flex space-between align-center gap-16">
    <h1 class="header-title">
      Добавление товара
    </h1>
    <div class="header__sort">
      <div class="select__container d-flex align-center">
        <select class="select">
          <option class="option" label="По умолчанию" value="1"></option>
          <option class="option" label="По наименованию" value="2"></option>
          <option class="option" label="По убыванию цены" value="3"></option>
          <option class="option" label="По возрастанию цены" value="4"></option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TheHeader"
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
