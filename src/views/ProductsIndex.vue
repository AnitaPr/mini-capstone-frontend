<script>
import axios from "axios";
export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("/products").then((response) => {
        console.log("products index", response);
        this.products = response.data;
      });
    },
  },
};
</script>

<template>
  <!-- <div class="products-index"> -->
  <div class="home-row">
    <h1 v-bind:class="className">{{ message }} count: {{ products.length }}</h1>
    <h1 class="m-3">{{ message }}</h1>
    <div v-for="product in products" v-bind:key="product.id">
      <div class="card" style="width: 20rem">
        <h2>{{ product.name }}</h2>
        <img
          v-bind:src="product.images[0].url"
          style="max-width 30px"
          v-if="product?.images && product?.images[0]?.url"
          v-bind:alt="product.name"
        />
        <p>Name: {{ product.name }}</p>
        <p>Price: {{ product.price }}</p>
        <p>Description: {{ product.description }}</p>
      </div>
    </div>
  </div>
</template>
