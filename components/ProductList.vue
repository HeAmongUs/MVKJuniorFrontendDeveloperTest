<template>
  <ul class="product-list d-flex gap-16 flex-wrap">
    <li v-for="product in productList" :key="product.id" class="product-list__item">
      <img :src="product.image" alt="" class="product-list__item-image">
      <div class="product-list__item__info">
        <div class="product-list__item__info-title">
          {{ product.title }}
        </div>
        <div class="product-list__item__info-description">
          {{ product.description }}
        </div>
        <div class="product-list__item__info-cost">
          {{ product.cost }}
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  name: "ProductList",
  props: {
    productList: {
      type: Array,
      required: true,
    }
  }
}
</script>

<style scoped lang="scss">
  .product-list {

    &__item {
      width: 332px;
      flex-grow: 1;
      max-width: 365px;
      box-shadow: 0 20px 30px #00000010, 0 6px 10px #00000010;

      &-image {
        width: 100%;
        height: 200px;
      }

      &__info {
        padding: 16px 16px 24px 16px;

        &-title {
          font-weight: 600;
          font-size: 20px;
          margin-bottom: 16px;
        }
        &-description {
          font-size: 16px;
          margin-bottom: 32px;
        }
        &-cost {
          font-size: 24px;
          font-weight: 600;

          &::after {
            content: '₽';
          }
        }
      }
    }
  }

  @media (max-width: 576px) {
    .product-list__item {
      width: 100%;
      max-width: none;
      &-image {
        height: 220px;
      }
    }
  }
</style>
