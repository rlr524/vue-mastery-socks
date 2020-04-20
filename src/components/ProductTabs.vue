<template>
  <div class="product-tabs">
    <span
      class="tab"
      :class="{ activeTab: selectedTab === tab }"
      v-for="(tab, index) in tabs"
      :key="index"
      @click="selectedTab = tab"
    >
      {{ tab }}
    </span>
    <div v-show="selectedTab === 'Reviews'">
      <p v-if="!reviews.length">There are no reviews yet.</p>
      <ul>
        <li v-for="(review, index) in reviews" :key="index">
          <p>{{ review.name }}</p>
          <p>Rating: {{ review.rating }}</p>
          <p>{{ review.review }}</p>
          <p>Recommended? {{ review.recommend }}</p>
        </li>
      </ul>
    </div>
    <ProductReview
      v-show="selectedTab === 'Leave a Review'"
      @review-submitted="addReview"
    />
  </div>
</template>

<script>
import ProductReview from "./ProductReview";

export default {
  components: {
    ProductReview,
  },
  data: function() {
    return {
      tabs: ["Reviews", "Leave a Review"],
      selectedTab: "Reviews",
      reviews: [],
    };
  },
  methods: {
    addReview: function(productReview) {
      this.reviews.push(productReview);
    },
  },
};
</script>

<style>
.tab {
  margin: 20px 10px 20px 0;
  cursor: pointer;
}

.activeTab {
  color: #16c0b0;
  text-decoration: underline;
}
</style>
