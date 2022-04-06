<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Wicked awesome store of things!",
      products: [],
      newProductParams: {},
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products.json").then((response) => {
        this.products = response.data;
        console.log("All products", this.products);
      });
    },
    createProduct: function () {
      console.log("Creating your product");

      axios.post("http://localhost:3000/products.json", this.newProductParams).then((response) => {
        console.log("Success", response.data);
        this.products.push(response.data);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
      <h1>List of Products</h1>
      <h2>Create that product!</h2>
      <div>
        name:
        <input type="text" v-model="newProductParams.name" />
        description:
        <input type="text" v-model="newProductParams.description" />
        price:
        <input type="text" v-model="newProductParams.price" />
        image_url:
        <input type="text" v-model="newProductParams.image_url" />
        <!-- </div> -->
      </div>
    </div>
    <button v-on:click="createProduct()">Create product</button>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>Name: {{ product.name }}</h2>
      <img v-bind:src="product.image_url" :alt="product.name" />
      <h4>Price: {{ product.price }}</h4>
    </div>
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>
