<template>
  <div id="product-review">
    <!-- we need to use .prevent to prevent default behavior so page won't reload on submit -->
    <form class="review-form" @submit.prevent="onSubmit">
      <p v-if="errors.length">
        <b>Please correct the following error(s):</b>
      </p>
      <ul>
        <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
      </ul>
      <p>
        <label for="name">Name:</label>
        <input id="name" v-model="name" placeholder="Your name" />
      </p>
      <p>
        <label for="review">Review:</label>
        <textarea
          id="review"
          v-model="review"
          placeholder="Leave a review..."
          cols="30"
          rows="10"
        ></textarea>
      </p>
      <p>
        <label for="rating">Rating:</label>
        <select id="rating" v-model.number="rating">
          <option>5</option>
          <option>4</option>
          <option>3</option>
          <option>2</option>
          <option>1</option>
        </select>
      </p>

      <p>Would you recommend this product?</p>
      <div class="recommend-radio">
        <span>
          <label for="yes">Yes</label>
          <input
            type="radio"
            name="recommend"
            id="yes"
            value="Yes"
            v-model="recommend"
          />
        </span>
        <span>
          <label for="no">No</label>
          <input
            type="radio"
            name="recommend"
            id="no"
            value="No"
            v-model="recommend"
          />
        </span>
      </div>
      <p>
        <input type="submit" value="Submit" />
      </p>
    </form>
  </div>
</template>

<script>
export default {
  name: "ProductReview",
  data: function() {
    return {
      name: null,
      review: null,
      rating: null,
      recommend: null,
      errors: [],
    };
  },
  methods: {
    onSubmit() {
      if (this.name && this.review && this.rating) {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating,
          recommend: this.recommend,
        };
        this.$emit("review-submitted", productReview);
        this.name = null;
        this.review = null;
        this.rating = null;
        this.recommend = null;
      } else {
        if (!this.name) this.errors.push("Name required!");
        if (!this.review) this.errors.push("Review required!");
        if (!this.rating) this.errors.push("Rating required!");
      }
    },
  },
};
</script>

<style>
.review-form {
  width: 400px;
  padding: 20px;
  margin: 40px 0;
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

.recommend-radio {
  display: flex;
}
</style>
