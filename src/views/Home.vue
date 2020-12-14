<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="createProduct()">Add Product</button>
    
    <div v-for="product in products">
      {{ product }}
      <p><img v-bind:src="product.image_url" v-bind:alt="product.title"></p>
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
    createProduct: function () {
      console.log("creating product...");
      var params = {
        name: "Baby Yoda",
        description: "Baby Yoda doll",
        image_url: "the image url",
        price: 45,
        tax: 5,
        total: 50,
      };
      axios.post("/api/products", params).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
      });
    },
  },
};
</script>