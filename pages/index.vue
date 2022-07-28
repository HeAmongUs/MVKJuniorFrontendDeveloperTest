<template>
  <div class="main-page">
    <transition name="slide-fade">
      <div v-if="isMessage" class="message">{{ textMessage }}</div>
    </transition>
    <the-header />
    <div class="d-flex gap-16 main">
      <the-sidebar @add-new-product="addNewProduct"/>
      <product-list :product-list="productList" @remove-item="removeItem"/>
    </div>
  </div>
</template>

<script>
import TheSidebar from "../components/TheSidebar";
import TheHeader from "../components/TheHeader";
import ProductList from "../components/ProductList";
export default {
  name: "Index",
  components: {ProductList, TheHeader, TheSidebar},
  data() {
    return {
      isMessage: false,
      textMessage: null,
      productList: [
        // {id: 1, title: "Название товара", cost: 10000, imgLink: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
        // {id: 2, title: "Название товара2", cost: 11000, imgLink: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
        // {id: 3, title: "Название товара3", cost: 12000, imgLink: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
        // {id: 4, title: "Товар1", cost: 2500, imgLink: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
        // {id: 5, title: "Товар2", cost: 4600, imgLink: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
      ]
    }
  },
  created() {
    this.productList = JSON.parse(localStorage.getItem('productList'))
  },
  methods: {
    addNewProduct(productToAdd) {
      const newProductId = Math.max(...this.productList.map((i) => i.id)) + 1
      productToAdd = {id: newProductId, ...productToAdd}
      this.productList.push(productToAdd)
      localStorage.setItem("productList", JSON.stringify(this.productList))

      this.showSuccessMessage("Успешно добавлено")
    },
    showSuccessMessage(text) {
      this.isMessage = true
      this.textMessage = text
      setTimeout(() => {
        this.isMessage = false
        this.textMessage = null
      }, 3000)
    },
    removeItem(productId) {
      this.productList = this.productList.filter(product => product.id !== productId)
      localStorage.setItem("productList", JSON.stringify(this.productList))

      this.showSuccessMessage("Успешно удалено")
    },
  },
}
</script>

<style scoped lang="scss">
.main-page {
  padding: 32px;
  background: $color-bg-body;
  height: 100vh;
}

.slide-fade-enter-active {
  transition: all 0.8s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter{
  transform: translateY(-20px);
  opacity: 0.5;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

.message {
  position: absolute;
  top: 40px;
  right: 40px;
  padding: 16px;
  font-size: 16px;
  color: $color-green;
  background: $color-bg-main;
  border: 1px solid $color-green;
  min-width: 100px;
  min-height: 50px;
  border-radius: 4px;
  box-shadow: 0 20px 30px #00000010, 0 6px 10px #00000010;
  z-index: 1000;
}

@media (max-width: 800px) {
  .main {
    flex-wrap: wrap;
  }
}
</style>
