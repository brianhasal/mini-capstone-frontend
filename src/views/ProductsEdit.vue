<script>
import axios from "axios"

  export default {
    data: function () {
      return {
        product: {},
        editProductParams: {
          supplier: {
            id: 0
          },
        },
        errors: []
      };
    },
    created: function () {
      axios
        .get("/products/" + this.$route.params.id + ".json")
        .then((response) => {
          console.log("Gathering Product", response);
          this.product = response.data;
          this.editProductParams = this.product;
        })
    },
    methods: {
      updateProduct: function(product) {
        axios
          .patch("/products/" + product.id +".json", this.editProductParams)
          .then((response) => {
            console.log("Product Editing", response);
            this.$router.push("/products")
          })
          .catch((error) => {
            console.log("error while updating", error.response);
            this.errors = error.response.data.errors;
          })
      }
    },
  };
</script>

<template>
  <div class="products-edit">
    <h1>Edit Product</h1>
    <form v-on:submit.prevent="updateProduct(product)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>    
      <div>
        Edit Name:
        <input v-model="editProductParams.name" type="text">
      </div>
      <div>
        Edit Price:
        <input v-model="editProductParams.price" type="text">
      </div>
      <div>
        Edit Description:
        <input v-model="editProductParams.description" type="text">
      </div>
      <div>
        Edit Supplier ID:
        <input v-model="editProductParams.supplier.id" type="text">
      </div>
      <input type="submit" value="Update" />
    </form>


  </div>
</template>

<style></style>