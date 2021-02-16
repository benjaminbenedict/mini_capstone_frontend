<template>
  <div class="prodcut-index">
    <h1>All Photos</h1>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
      <img v-bind:src="product.primary_image_url" v-bind:alt="product.name" />
      <p>price: {{ product.price }}</p>
      <p>description {{ product.description }}</p>
      <router-link v-bind:to="`/products/${product.id}`">More details</router-link>
    </div>
  </div>
</template>
<style scoped>
img {
  width: 300px;
}
</style>
<script>
import axios from "axios";
export default {
  data: function() {
    return {
      products: [],
    };
  },
  created: function() {
    axios.get("/api/products").then(response => {
      console.log("products index", response);
      this.products = response.data;
    });
  },
  methods: {},
};
</script>
