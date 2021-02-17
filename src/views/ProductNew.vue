<template>
  <div class="products-new">
    <h1>New Product</h1>
    <form v-on:submit.prevent="createProduct()">
      <ul>
        <li v-for="error in errors" :key="error">{{ error }}</li>
        <img v-if="status" v-bind:src="`https://http.cat/${status}`" v-on:click="status = ''" alt="" />
      </ul>
      Name:
      <input type="text" v-model="newProductName" />
      Price:
      <input type="text" v-model="newProductPrice" />
      Description:
      <input type="text" v-model="newProductDescription" />
      Supplier_id:
      <input type="text" v-model="newProductSupplier_id" />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      newProductName: "",
      newProductPrice: "",
      newProductDescription: "",
      newProductSupplier_id: "",
      status: "",
      errors: [],
    };
  },
  created: function() {},
  methods: {
    createProduct: function() {
      var params = {
        name: this.newProductName,
        Price: this.newProductPrice,
        Description: this.newProductDescription,
        Supplier_id: this.newProductSupplier_id,
      };
      axios
        .post("/api/products", params)
        .then(response => {
          console.log("products create", response);
          this.$router.push("/products");
        })
        .catch(error => {
          console.log("products create error", error.response);
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>
