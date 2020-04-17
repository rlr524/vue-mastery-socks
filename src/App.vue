<template>
  <div id="app">
    <div class="nav-bar"></div>
    <div class="product">
      <div class="product-image">
        <img :src="image" alt="Socks">
      </div>
      <div class="product-info">
        <h1>{{product}}</h1>
        <a :href="vendor" target="_blank">Get from Nordstrom</a>
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost Out</p>
        <p v-else>Out of Stock</p>
        <p v-show="onSale">On Sale!</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data: function() {
    // note the way the URLs are handled...if you're pointing to an internal asset, you need a require just as in 
    // if you're pointing to an external URL, you can't have the require...has to do with how webpack
    // handles these URLs and only matters in a vue file (not an HTML and js combo)
    return {
      product: "Socks",
      image: require("./assets/vmSocks-green-onWhite.jpg"),
      vendor: "https://www.nordstrom.com",
      inStock: false,
      inventory: 0,
      onSale: false
    }
  }
}
</script>

<style>
 body {
    font-family: tahoma;
    color:#282828;
    margin: 0px;
  }
  
  .nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
  }

  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
  }

  img {
    border: 1px solid #d8d8d8;
    width: 70%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
  }
  
  .product-image {
    width: 80%;
  }

  .product-vendor {
    padding-top: 1px;
  }
  
  .product-image,
  .product-info {
    margin-top: 10px;
    width: 50%;
  }

  h1 {
    margin-bottom: 2px;
  }
  
  .color-box {
    width: 40px;
    height: 40px;
    margin-top: 5px;
  }
  
  .cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }
  
  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  } 
  
  .disabledButton {
    background-color: #d8d8d8;
  }
  
  .review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
  }
  
  input {
    width: 100%;  
    height: 25px;
    margin-bottom: 20px;
  }
  
  textarea {
    width: 100%;
    height: 60px;
  }

  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }
</style>
