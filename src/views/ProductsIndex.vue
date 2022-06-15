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
        axios.get("/products.json").then((response) => {
          console.log("products index", response);
          this.products = response.data;
        });
      },
    },
  };
</script>

<template>
  <div class="products-index">
    <h1>Products Index</h1>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
    </div>
  </div>
</template>

<style></style>