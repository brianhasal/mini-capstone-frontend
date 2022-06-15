<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        product: {},
      };
    },
    created: function () {
      axios
        .get("/products/" + this.$route.params.id + ".json")
        .then((response) => {
          console.log("showing product", response);
          this.product = response.data;
        })
    },
    methods: {},
  };
</script>

<template>
  <div class="products-show">
    <h1>Product Details</h1>
    <h2>Name: {{product.name}}</h2>
  </div>
</template>

<style></style>