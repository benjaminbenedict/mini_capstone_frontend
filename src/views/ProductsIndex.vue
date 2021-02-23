<template>
  <div class="prodcut-index">
    <h1>All Products</h1>
    Search by name:
    <input v-model="nameFilter" type="text" list="product-names" />
    <datalist id="product-names">
      <option v-for="product in products" v-bind:key="product.id">{{ product.name }}</option>
    </datalist>
    <div class="row row-cols-1 row-cols-md-3">
      <div class="col mb-4">
        <div v-for="product in filterBy(products, nameFilter, 'name')" v-bind:key="product.id" class="card">
          <img v-bind:src="product.primary_image_url" class="card-img-top" v-bind:alt="product.name" />
          <div class="card-body">
            <h5 class="card-title">{{ product.name }}</h5>
            <p class="card-text">{{ product.description }}</p>
            <router-link v-bind:to="`/products/${product.id}`">More details</router-link>
          </div>
        </div>
      </div>
      <!-- <div v-for="product in filterBy(products, nameFilter, 'name')" v-bind:key="product.id">
        <h2>{{ product.name }}</h2>
        <img v-bind:src="product.primary_image_url" v-bind:alt="product.name" />
        <p>price: {{ product.price }}</p>
        <p>description {{ product.description }}</p>
        <router-link v-bind:to="`/products/${product.id}`">More details</router-link>
      </div> -->
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
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      products: [],
      nameFilter: "",
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
