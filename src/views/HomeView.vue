<script>
import axios from 'axios';

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      name: "samuel",
      products: []
    };
  },
  created: function() {},
  methods: {
    indexProducts: function() {
      console.log('getting the data...');
      axios.get("http://localhost:3000/products.json").then(response => {
        console.log(response.data);
        this.products = response.data
      } )
    }
  }
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
     <h3>{{ name }}</h3>
     <!-- <h3>{{ products }}</h3> -->
     <div v-for="product in products">
     <p>{{ product.name }}</p>
      <p>{{ product.description }}</p>
     <br />
     <br />
     <br />
     </div>
<button v-on:click="indexProducts()">get index products</button>
  </div>
</template>
