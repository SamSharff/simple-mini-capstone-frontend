<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Wicked awesome store of things!",
      products: [],
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
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <div>
      <h1>List of Products</h1>
    </div>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>Name: {{ product.name }}</h2>
      <h4>Price: {{ product.price }}</h4>
    </div>
  </div>
</template>

<style></style>
