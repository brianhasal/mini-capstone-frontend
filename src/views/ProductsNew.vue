<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        product: {},
        newProductParams: {},
        errors: []
      };
    },
    created: function () {},
    methods: {
      createProduct: function () {
        axios
          .post("/products/new", this.newProductParams)
          .then((response) => {
            console.log("product created", response);
            this.product = response.data;
            this.$router.push("/products/" + this.product.id);
          })
          .catch((error) => {
            console.log("product create error", error.response);
            this.errors = error.response.data.errors;
          });
      }
    },
  };
</script>

<template>
  <div class="product-create">
    <h1>Product Create Page</h1>
    <form v-on:submit.prevent="createProduct()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        Product Name: 
        <input v-model="newProductParams.name" type="text">
      </div>
      <div>
        Product Price: 
        <input v-model="newProductParams.price" type="text">
      </div>
      <div>
        Product Description: 
        <input v-model="newProductParams.description" type="text">
      </div>
      <div>
        Supplier ID:
        <input v-model="newProductParams.supplier_id" type="text">
      </div>
      <input type="submit" value="Create Product" />
    </form>
  </div>
</template>

<style></style>