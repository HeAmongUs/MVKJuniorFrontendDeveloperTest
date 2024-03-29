<template>
  <TransitionGroup name="product-list" tag="ul" class="product-list d-flex gap-16 flex-wrap">
    <li v-for="product in productList" :key="product.id" class="product-list__item">
      <img :src="product.imgLink" alt="" class="product-list__item-image">
      <div class="product-list__item__info">
        <div class="product-list__item__info-title">
          {{ product.title }}
        </div>
        <div class="product-list__item__info-description">
          {{ product.description }}
        </div>
        <div class="product-list__item__info-cost">
          {{ product.cost.toLocaleString() }}
        </div>
      </div>
      <div class="product-list__item__delete" @click="removeItem(product.id)">
        <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
          <path d="M10.207 5.79681C10 5.79681 9.83228 5.96455 9.83228 6.17152V13.2535C9.83228 13.4603 10 13.6282 10.207 13.6282C10.4139 13.6282 10.5817 13.4603 10.5817 13.2535V6.17152C10.5817 5.96455 10.4139 5.79681 10.207 5.79681Z"/>
          <path d="M5.78547 5.79681C5.57851 5.79681 5.41077 5.96455 5.41077 6.17152V13.2535C5.41077 13.4603 5.57851 13.6282 5.78547 13.6282C5.99244 13.6282 6.16018 13.4603 6.16018 13.2535V6.17152C6.16018 5.96455 5.99244 5.79681 5.78547 5.79681Z" />
          <path d="M2.56301 4.76329V13.9953C2.56301 14.5409 2.76309 15.0534 3.11262 15.421C3.46054 15.7898 3.94473 15.9991 4.45147 15.9999H11.541C12.0479 15.9991 12.5321 15.7898 12.8799 15.421C13.2294 15.0534 13.4295 14.5409 13.4295 13.9953V4.76329C14.1243 4.57887 14.5745 3.90762 14.4816 3.19465C14.3885 2.48183 13.7812 1.94861 13.0622 1.94846H11.1438V1.48008C11.146 1.0862 10.9902 0.707978 10.7114 0.429729C10.4326 0.151627 10.0538 -0.00323193 9.65988 -1.18018e-05H6.33261C5.93873 -0.00323193 5.55992 0.151627 5.28109 0.429729C5.00225 0.707978 4.84652 1.0862 4.84871 1.48008V1.94846H2.93025C2.21128 1.94861 1.60399 2.48183 1.5109 3.19465C1.41796 3.90762 1.86819 4.57887 2.56301 4.76329ZM11.541 15.2505H4.45147C3.81081 15.2505 3.31242 14.7002 3.31242 13.9953V4.79623H12.6801V13.9953C12.6801 14.7002 12.1817 15.2505 11.541 15.2505ZM5.59812 1.48008C5.59564 1.28497 5.67233 1.09717 5.8108 0.959441C5.94912 0.821707 6.13735 0.746034 6.33261 0.7494H9.65988C9.85514 0.746034 10.0434 0.821707 10.1817 0.959441C10.3202 1.09703 10.3969 1.28497 10.3944 1.48008V1.94846H5.59812V1.48008ZM2.93025 2.69787H13.0622C13.4348 2.69787 13.7367 2.99983 13.7367 3.37234C13.7367 3.74485 13.4348 4.04681 13.0622 4.04681H2.93025C2.55774 4.04681 2.25578 3.74485 2.25578 3.37234C2.25578 2.99983 2.55774 2.69787 2.93025 2.69787Z"/>
          <path d="M7.99617 5.79681C7.7892 5.79681 7.62146 5.96455 7.62146 6.17152V13.2535C7.62146 13.4603 7.7892 13.6282 7.99617 13.6282C8.20313 13.6282 8.37087 13.4603 8.37087 13.2535V6.17152C8.37087 5.96455 8.20313 5.79681 7.99617 5.79681Z" />
        </svg>
      </div>
    </li>
  </TransitionGroup>
</template>

<script>
export default {
  name: "ProductList",
  props: {
    productList: {
      type: Array,
      required: true,
    }
  },
  emits: ['remove-item'],
  methods: {
    removeItem(productId) {
      this.$emit('remove-item', productId)
    }
  }
}
</script>

<style scoped lang="scss">
  .product-list-move,
  .product-list-enter-active,
  .product-list-leave-active {
    transition: all 0.5s ease;
  }
  .product-list-enter-from,
  .product-list-leave-to {
    opacity: 0;
    transform: translateX(30px);
  }

  .product-list {

    &__item {
      position: relative;
      width: 332px;
      flex-grow: 1;
      max-width: 365px;
      box-shadow: 0 20px 30px #00000010, 0 6px 10px #00000010;

      &:hover {
        .product-list__item__delete {
          opacity: 1;
        }
      }

      &-image {
        width: 100%;
        height: 200px;
      }
      &__delete {
        opacity: 0;
        position: absolute;
        top: -8px;
        right: -8px;
        width: 32px;
        height: 32px;
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
        border-radius: 10px;
        background: $color-red;
        transition: 0.3s;
        cursor: pointer;
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
            content: 'руб.';
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
