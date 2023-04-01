<template>
  <div>
    <form class="review-form" @submit.prevent="onSubmit">
      <div class="errorMessage" v-if="errors.length">
        <h3>Please correct the following error (s)</h3>
        <ul>
          <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
        </ul>
      </div>
      <div class="row">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="name" />
      </div>
      <div class="row">
        <label for="review">Review:</label>
        <textarea id="review" v-model="review"></textarea>
      </div>
      <div class="row">
        <label for="rating">Rating:</label>
        <select id="rating" v-model.number="rating">
          <option>5</option>
          <option>4</option>
          <option>3</option>
          <option>2</option>
          <option>1</option>
        </select>
      </div>
      <div class="row">
        <button type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
import { eventBus } from "../main.js";
export default {
  name: "Product-review",
  data() {
    return {
      name: null,
      rating: null,
      review: null,
      errors: [],
    };
  },
  methods: {
    onSubmit() {
      this.errors = [];
      if (this.rating && this.name && this.review) {
        let productReview = {
          name: this.name,
          rating: this.rating,
          review: this.review,
        };
        eventBus.$emit("review-submitted", productReview);
        this.name = null;
        this.rating = null;
        this.review = null;
      } else {
        if (!this.name) this.errors.push("Name required");
        if (!this.rating) this.errors.push("Rating required");
        if (!this.review) this.errors.push("Review required");
      }
    },
  },
};
</script>
