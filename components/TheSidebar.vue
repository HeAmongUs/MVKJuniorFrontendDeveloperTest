<template>
    <div class="sidebar d-flex flex-column gap-16">
      <div class="sidebar__item">
        <div class="sidebar__item-title required">Наименование товара</div>
        <div class="sidebar__item__input">
          <input type="text" placeholder="Введите наименование товара" class="sidebar__item__input-input" />
          <div class="bar"></div>
        </div>
      </div>
      <div class="sidebar__item">
        <div class="sidebar__item-title">Описание товара</div>
        <div class="sidebar__item__input">
          <textarea placeholder="Введите описание товара" class="sidebar__item__input-textarea" />
          <div class="bar"></div>
        </div>
      </div>
      <div class="sidebar__item">
        <div class="sidebar__item-title required">Ссылка на изображение товара</div>
        <div class="sidebar__item__input">
          <input type="text" placeholder="Введите ссылку" class="sidebar__item__input-input" />
          <div class="bar"></div>
        </div>
      </div>
      <div class="sidebar__item">
        <div class="sidebar__item-title required">Цена товара</div>
        <div class="sidebar__item__input">
          <input type="text" placeholder="Введите цену" class="sidebar__item__input-input" />
          <div class="bar"></div>
        </div>
      </div>
      <input type="button" value="Добавить товар" class="sidebar-submit">
    </div>
</template>

<script>
export default {
    name: 'TheSidebar',
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
    box-shadow: 0 20px 30px #00000010, 0 6px 10px #00000010;

    &__item {
      position: relative;
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
      top: 0;
      right: -5px;
      width: 4px;
      height: 4px;
      border-radius: 50%;
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
