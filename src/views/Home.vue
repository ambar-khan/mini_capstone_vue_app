<template>
  <div class="home">
    <h1>{{ message }}</h1>
  
    <h2>Add a new product</h2>
    <p>Name:<input type='text' v-model='name'></p>
    <p>Description:<input type='text' v-model='description'></p>
    <p>Image_url:<input type='text' v-model='image_url'></p>
    <p>Price:<input type='text' v-model='price'></p>
    <button v-on:click="createProduct()">Add Product</button>

    <br>

  <div v-for="product in products">
      {{ product.id }}
      {{ product.title }}
      <p><img v-bind:src="product.image_url" v-bind:alt="product.title"></p>
      <button v-on:click="showProduct(product)">Show more info</button>
      <hr>
    </div>
    
    <dialog id="product-details">
      <form method="dialog">
        <h3>Hello</h3>
        <p><strong>name:</strong> {{ currentProduct.name }}</p>
        <p><strong>description:</strong> {{ currentProduct.description }}</p>
        <p><strong>image_url:</strong> {{ currentProduct.image_url }}</p>
        <p><strong>price:</strong> {{ currentProduct.price }}</p>
        <p><strong>tax:</strong> {{ currentProduct.tax }}</p>
        <p><strong>total:</strong> {{ currentProduct.total }}</p>
        <button>Close</button>
        
      </form>
    </dialog>  
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
      currentProduct: {},
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
    showProduct: function (theProduct) {
      console.log(theProduct);
      this.currentProduct = theProduct;
      console.log("show product...");
      document.querySelector("#product-details").showModal();
    },
  },
};
</script>