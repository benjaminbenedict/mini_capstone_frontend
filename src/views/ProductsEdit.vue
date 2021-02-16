<template>
  <div class="products-edit">
    <h1>Edit Product</h1>
    <form v-on:submit.prevent="updateProduct(product)">
      <ul>
        <li v-for="error in errors" :key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="product.name" />
      price:
      <input type="text" v-model="product.price" />
      description:
      <input type="text" v-model="product.description" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      product: {},
      errors: [],
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id).then(response => {
      console.log("products show", response);
      this.product = response.data;
    });
  },
  methods: {
    updateProduct: function(product) {
      var params = {
        name: product.name,
        price: product.price,
        description: product.description,
      };
      axios
        .patch("/api/products/" + product.id, params)
        .then(response => {
          console.log("products update", response);
          this.$router.push("/products");
        })
        .catch(error => {
          console.log("products update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
