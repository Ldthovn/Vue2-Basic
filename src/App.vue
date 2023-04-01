<template>
  <div id="app">
    <header id="header">
      <div class="container">
        <div class="cart">
          <p>
            <i class="fas fa-shopping-cart"></i>
            {{ cart.length }}
          </p>
        </div>
      </div>
    </header>
    <Product :member="member" @addToCart="updateCart" />
  </div>
</template>

<script>
import Product from "./components/Product.vue";

export default {
  name: "App",
  components: {
    Product,
  },
  data() {
    return {
      member: false,
      cart: [],
    };
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
  },
};
</script>
