<template>
  <div id="product">
    <div class="product">
      <div class="product-image">
        <img :src="image" alt="Socks" />
      </div>
      <div class="product-info">
        <h1>{{ productTitle }}</h1>
        <a :href="vendor" target="_blank">Get from Nordstrom</a>
        <p v-if="inStock">In Stock</p>
        <p v-else :class="{ outStockLabel: !inStock }">Out of Stock</p>
        <p v-if="onSale">On Sale!</p>
        <Shipping :shipping="shipping" />
        <span>Product details:</span>
        <ProductDetails :details="details"></ProductDetails>
        <p>Available colors:</p>
        <div
          v-for="(variant, index) in variants"
          :key="variant.variantId"
          class="color-box"
          :style="{ backgroundColor: variant.variantColor }"
          @mouseover="updateProduct(index)"
        ></div>
        <p>
          Available in sizes:
          <span v-for="(size, index) in sizes" :key="index">
            {{ size }}
          </span>
        </p>
        <div class="cart-buttons">
          <button
            @click="addToCart"
            :disabled="!inStock"
            :class="{ disabledButton: !inStock }"
          >
            Add to Cart
          </button>
          <button @click="removeFromCart">
            Remove from Cart
          </button>
        </div>
        <ProductTabs />
      </div>
    </div>
  </div>
</template>

<script>
import ProductDetails from "./ProductDetails";
import ProductTabs from "./ProductTabs";
import Shipping from "./Shipping";

export default {
  name: "Product",
  components: {
    ProductDetails,
    ProductTabs,
    Shipping,
  },

  data: function() {
    // note the way the URLs are handled...if you're pointing to an internal asset, you need a require just as in
    // if you're pointing to an external URL, you can't have the require...has to do with how webpack
    // handles these URLs and only matters in a vue file (not an HTML and js combo)
    return {
      brand: "Vue Mastery",
      product: "Socks",
      selectedVariant: 0,
      vendor: "https://www.nordstrom.com",
      variants: [
        {
          variantId: 2234,
          variantColor: "green",
          variantImage: require("../assets/vmSocks-green-onWhite.jpg"),
          variantQuantity: 22,
          variantSale: true,
        },
        {
          variantId: 2235,
          variantColor: "blue",
          variantImage: require("../assets/vmSocks-blue-onWhite.jpg"),
          variantQuantity: 11,
          variantSale: false,
        },
      ],
      sizes: ["s", "m", "l", "xl", "xxl"],
      details: ["80% Cotton", "20% Polyester", "Gender-neutral"],
    };
  },
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    addToCart: function() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].variantId);
    },
    removeFromCart: function() {
      this.$emit(
        "remove-from-cart",
        this.variants[this.selectedVariant].variantId
      );
    },
    updateProduct: function(index) {
      this.selectedVariant = index;
      console.log(index);
    },
  },
  computed: {
    productTitle() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    onSale() {
      return this.variants[this.selectedVariant].variantSale;
    },
    shipping() {
      return this.premium ? "Free" : "$" + 2.99;
    },
  },
};
</script>

<style>
.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px #d8d8d8;
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

.size-text {
  margin: 10px 0;
}

.color-box {
  display: inline-block;
  width: 40px;
  height: 40px;
  margin-right: 5px;
  margin-top: 5px;
}

.cart-buttons {
  display: flex;
}

button {
  margin-top: 5px;
  border: none;
  background-color: #1e95ea;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
  margin-right: 5px;
  margin-bottom: 15px;
}

.disabledButton {
  background-color: #d8d8d8;
}

.outStockLabel {
  text-decoration: line-through;
}
</style>
