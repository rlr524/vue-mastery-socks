<template>
  <div id="app">
    <div class="header">
      <div class="premium" v-bind:class="{ hidden: !premium }">
        YOU HAVE PREMIUM STATUS
      </div>
      <div class="cart">Cart({{ cart.length }})</div>
    </div>
    <Product
      @add-to-cart="updateCart"
      @remove-from-cart="refreshCart"
      :premium="premium"
    />
  </div>
</template>
<script>
import Product from "./components/Product";
export default {
  name: "App",
  data: function() {
    return {
      premium: true,
      cart: [],
    };
  },
  components: {
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

.header {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
  padding-top: 25px;
}

.cart {
  color: #ffffff;
  margin-right: 15px;
  float: right;
  border: 1px solid #ffffff;
  padding: 5px 20px;
}

.premium {
  color: #ffffff;
  margin-right: 15px;
  border: 1px solid #ffffff;
  padding: 5px 20px;
  float: right;
}

.hidden {
  display: none;
}
</style>
