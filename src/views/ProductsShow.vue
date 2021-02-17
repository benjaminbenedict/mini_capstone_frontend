<template>
  <div class="products-show">
    <h2>{{ product.name }}</h2>
    <img v-bind:src="product.id" v-bind:alt="product.name" />
    <p>name: {{ product.name }}</p>
    <p>description: {{ product.description }}</p>
    <router-link v-if="product.is_admin" v-bind:to="`/products/${product.id}/edit`">Edit product</router-link>
    <button v-if="product.is_admin" v-on:click="destroyProduct(product)">Destroy product</button>
    <router-link to="/products">Back to all products</router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      product: {},
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id).then(response => {
      console.log("products show", response);
      this.product = response.data;
    });
  },
  methods: {
    destroyProduct: function(product) {
      axios.delete("/api/products/" + product.id).then(response => {
        console.log("products destroy", response);
        this.$router.push("/products");
      });
    },
  },
};
</script>
