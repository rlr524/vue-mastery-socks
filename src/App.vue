<template>
  <div id="app">
    <div class="cart">
      <p>Cart({{ cart.length }})</p>
    </div>
    <Header />
    <Product
      :premium="premium"
      @add-to-cart="updateCart"
      @remove-from-cart="refreshCart"
    />
    <Product
      :premium="premium"
      @add-to-cart="updateCart"
      @remove-from-cart="refreshCart"
    />
    <Product
      :premium="premium"
      @add-to-cart="updateCart"
      @remove-from-cart="refreshCart"
    />
  </div>
</template>
<script>
import Header from "./components/Header";
import Product from "./components/Product";
export default {
  name: "App",
  data: function() {
    return {
      premium: false,
      cart: [],
    };
  },
  components: {
    Header,
    Product,
  },
  methods: {
    updateCart: function(id) {
      this.cart.push(id);
    },
    refreshCart: function(id) {
      for (var i = this.cart.length - 1; i >= 0; i--) {
        if (this.cart[i] === id) {
          this.cart.splice(i, 1);
        }
      }
    },
  },
};
</script>

<style>
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.cart {
  color: #ffffff;
  margin-right: 25px;
  float: right;
  border: 1px solid #ffffff;
  padding: 5px 20px;
}
</style>
