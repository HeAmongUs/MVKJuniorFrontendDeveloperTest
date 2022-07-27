<template>
  <div class="main-page">
    <the-header />
    <div class="d-flex gap-16 main">
      <the-sidebar />
      <product-list :product-list="productList"/>
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
      productList: [
        {id: 1, title: "Название товара", cost: "10000", image: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
        {id: 2, title: "Название товара2", cost: "11000", image: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
        {id: 3, title: "Название товара3", cost: "12000", image: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
        {id: 4, title: "Товар1", cost: "2500", image: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
        {id: 5, title: "Товар2", cost: "4600", image: "https://i.ibb.co/TTSPftz/Rectangle-31.png", description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"},
      ]
    }
  }

}
</script>

<style scoped lang="scss">
.main-page {
  padding: 32px;
  background: $color-bg-body;
  height: 100vh;
}

@media (max-width: 800px) {
  .main {
    flex-wrap: wrap;
  }
}
</style>
