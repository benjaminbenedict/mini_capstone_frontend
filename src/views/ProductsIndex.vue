<template>
  <div class="prodcut-index">
    <h1>All Products</h1>
    Search by name:
    <input v-model="nameFilter" type="text" list="product-names" />
    <datalist id="product-names">
      <option v-for="product in products" v-bind:key="product.id">{{ product.name }}</option>
    </datalist>

    <div class="row row-cols-1 row-cols-md-3">
      <div v-for="product in filterBy(products, nameFilter, 'name')" v-bind:key="product.id" class="col mb-4">
        <div class="card">
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
.cta-100 {
  margin-top: 100px;
  padding-left: 8%;
  padding-top: 7%;
}
.col-md-4 {
  padding-bottom: 20px;
}

.white {
  color: #fff !important;
}
.mt {
  float: left;
  margin-top: -20px;
  padding-top: 20px;
}
.bg-blue-ui {
  background-color: #708198 !important;
}
figure img {
  width: 300px;
}

#blogCarousel {
  padding-bottom: 100px;
}

.blog .carousel-indicators {
  left: 0;
  top: -50px;
  height: 50%;
}

/* The colour of the indicators */

.blog .carousel-indicators li {
  background: #708198;
  border-radius: 50%;
  width: 8px;
  height: 8px;
}

.blog .carousel-indicators .active {
  background: #0fc9af;
}

.item-carousel-blog-block {
  outline: medium none;
  padding: 15px;
}

.item-box-blog {
  border: 1px solid #dadada;
  text-align: center;
  z-index: 4;
  padding: 20px;
}

.item-box-blog-image {
  position: relative;
}

.item-box-blog-image figure img {
  width: 100%;
  height: auto;
}

.item-box-blog-date {
  position: absolute;
  z-index: 5;
  padding: 4px 20px;
  top: -20px;
  right: 8px;
  background-color: #41cb52;
}

.item-box-blog-date span {
  color: #fff;
  display: block;
  text-align: center;
  line-height: 1.2;
}

.item-box-blog-date span.mon {
  font-size: 18px;
}

.item-box-blog-date span.day {
  font-size: 16px;
}

.item-box-blog-body {
  padding: 10px;
}

.item-heading-blog a h5 {
  margin: 0;
  line-height: 1;
  text-decoration: none;
  transition: color 0.3s;
}

.item-box-blog-heading a {
  text-decoration: none;
}

.item-box-blog-data p {
  font-size: 13px;
}

.item-box-blog-data p i {
  font-size: 12px;
}

.item-box-blog-text {
  max-height: 100px;
  overflow: hidden;
}

.mt-10 {
  float: left;
  margin-top: -10px;
  padding-top: 10px;
}

.btn.bg-blue-ui.white.read {
  cursor: pointer;
  padding: 4px 20px;
  float: left;
  margin-top: 10px;
}

.btn.bg-blue-ui.white.read:hover {
  box-shadow: 0px 5px 15px inset #4d5f77;
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
