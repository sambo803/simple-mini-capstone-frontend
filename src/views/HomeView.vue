<script>
import axios from 'axios';

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      name: "samuel",
      products: [],
      newProduct: {}
    };
  },
  created: function() {
    this.indexProducts();
  },
  methods: {
    indexProducts: function() {
      console.log('getting the data...');
      axios.get("http://localhost:3000/products.json").then(response => {
        console.log(response.data);
        this.products = response.data
      } )
    },
    createProduct: function() {
      console.log('getting the data');
      var params = {
      name: this.newProduct.name,
      price: this.newProduct.price,
      description: this.newProduct.description,
      image_url: this.newProduct.image_url
      }
      axios.post("http://localhost:3000/products.json", params).then(response => {
        console.log(response.data);
        this.products.push(response.data);
      })
    },
    showProduct: function(theProduct) {
      console.log('getting the product...');
      console.log(theProduct);
      document.querySelector('#product-details').showModal();
    },
    updateProduct: function() {
      console.log("'updating product...");
      axios.patch("http://localhost:3000/products/11.json", {name: "Mega Chisel II"}).then(response => {
        console.log(response.data)
      })
    }

    //  ` destroyProduct: function() {
    //   console.log('destroying the product...');
    //   axios.delete("http://localhost:3000/products.json/8").then(response => {
    //     console.log(response.data);
    //     this.products = response.data
    //   } )
    // },`
  }
};


F
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
     <h3>{{ name }}</h3>
      <hr />
     <hr />
     <p>Name: <input type="text" v-model="newProduct.name" /></p>
     <p>description: <input type="text" v-model="newProduct.description" /></p>
     <p>price: <input type="text" v-model="newProduct.price" /></p>
     <p>image_url: <input type="text" v-model="newProduct.image_url" /></p>
     <button v-on:click="createProduct">Make new product</button>
    <hr/>
    <hr/>
     <!-- <h3>{{ products }}</h3> -->
     <div v-for="product in products">
     <p>{{ product.name }}</p>
      <p>{{ product.description }}</p>
      <p>{{ product.price }}</p>
      <p>{{ product.image_url }}</p>
      <button v-on:click="showProduct">More Info</button>
      <!-- <p>{{ product.description }}</p> -->
     <br />
     <br />
     <br />
     </div>

     <dialog> id="product-details">
     <form method="dialog">
     <p><b>name:</b> {{currentProduct.name}}</p>
     <p><b>description:</b> {{currentProduct.description}}</p>
     <p><b>price:</b> {{currentProduct.price}}</p>
     <p><b>image_url:</b> {{currentProduct.image_url}}</p>
     <button v-on:click="updateProduct()">Update Product</button> 
     <button>Close</button>
     </form>
     </dialog>
<!-- <p><button v-on:click="indexProducts()">get index products</button></p> -->
<br/>


<div><button v-on:click="destroyProduct()">delete destroy product</button></div>p>
<br/>


  </div>
</template>
