<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="product in products">
      {{ product.name }}
    </div>
  </div>
</template>
<style>
</style>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Products Page",
      products: [],
    };
  },
  created: function () {
    console.log("in created");
    this.productsIndex();
  },
  methods: {
    productsIndex: function () {
      console.log("products index..");
      axios.get("/api/products").then((response) => {
        console.log(response.data);
        this.products = response.data;
      });
    },
  },
};
</script>
