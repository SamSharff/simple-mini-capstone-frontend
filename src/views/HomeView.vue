<script>
export default {
  data: function () {
    return {
      message: "Wicked awesome store of things!",
      products: [
        { id: 1, name: "Shakespeare plays", price: 10 },
        { id: 2, name: "Jane Austen collection", price: 15 },
        { id: 3, name: "Charles Dickens: a collection", price: 20 },
      ],
    };
  },
  created: function () {},
  methods: {},
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
