<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Wicked awesome store of things!",
      products: [],
      newProductParams: {},
      currentProduct: {},
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
    showProduct: function (product) {
      console.log(product);
      this.currentProduct = product;
      document.querySelector("#product-details").showModal();
    },
    updateProduct: function (product) {
      var editProductParams = product;
      axios.patch("http://localhost:3000/products/" + product.id + ".json", editProductParams).then((response) => {
        console.log("Sucessfully updated!", response.data);
      });
    },
    destroyProduct: function (product) {
      axios.delete("http://localhost:3000/products/" + product.id).then((response) => {
        console.log("Product DESTROYEDDDDDDDDDDDD!", response.data);
        var index = this.products.indexOf(product);
        this.products.splice(index, 1);
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
      <button v-on:click="showProduct(product)">More info!</button>
    </div>
    <dialog id="product-details">
      <form method="dialog">
        <h1>Product Info</h1>
        <p>
          Name:
          <input type="text" v-model="currentProduct.name" />
        </p>
        <p>
          Description:
          <input type="text" v-model="currentProduct.description" />
        </p>
        <p>
          Price:
          <input type="text" v-model="currentProduct.price" />
        </p>
        <button>Close details</button>
        <button v-on:click="updateProduct(currentProduct)">Update Product</button>
        <button v-on:click="destroyProduct(currentProduct)">Destroy Product</button>
      </form>
    </dialog>
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>
