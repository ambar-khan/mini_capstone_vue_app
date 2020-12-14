<template>
  <div class="home">
    <h1>{{ message }}</h1>
  
    <h2>Add a new product</h2>
    <p>Name:<input type='text' v-model='name'></p>
    <p>Description:<input type='text' v-model='description'></p>
    <p>Image_url:<input type='text' v-model='image_url'></p>
    <p>Price:<input type='text' v-model='price'></p>
    <button v-on:click="createProduct()">Add Product</button>

  <div v-for="product in products">
      {{ product.title }}
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
      name: "",
      description: "",
      image_url: "",
      price: "",
      tax: "",
      total: "",
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
        name: this.name,
        description: this.description,
        image_url: this.image_url,
        price: this.price,
      };
      axios.post("/api/products", params).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
      });
    },
  },
};
</script>