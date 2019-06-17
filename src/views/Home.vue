<template>
  <div class="home">
        <ul>
          <li v-for="error in errors">{{ error }}</li>
        </ul>
    <h1>{{ message }}</h1>
    <div v-for="product in products">
      <h3>{{ product.name }}</h3>
      <h3>{{ product.description }}</h3>
      <router-link v-bind:to="'/products/' + product.id">
 
      <button class="btn btn-success" v-on:click="showProduct(product)">More Info</button>
           </router-link>
    </div>
    
    <h4>Edit Product</h4>
    <div v-for="product in products">
      <div>Product object: {{ product }}</div>
      <div>Name: <input type="text" v-model="product.name" /></div>
      <div>Description: <input type="text" v-model="product.description" /></div>
          <button class="btn btn-warning" v-on:click="updateProduct(product)">Update</button>
	    		<button class="btn btn-danger" v-on:click="destroyProduct(product)">Destroy</button>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Ben's Store",
      products: [],
      currentProduct: {},
      errors: []
    };
  },
  created: function() {
    axios.get("/api/products").then(response => {
      this.products = response.data;
      console.log(this.products);
    });
  },
  methods: {
  	showProduct: function(product) {
  		if (this.currentProduct === product) {
  			this.currentProduct = null;
  		} else {
				this.currentProduct = product;
  		}
  	},
  	updateProduct: function(product) {
  		// send a patch request to the backend to update this product!
  		var params = {
        name: product.name,
        description: product.description
  		};
  		axios.patch("/api/products/" + product.id, params).then(response => {
  			console.log("Success!", response.data);
  			// product = response.data;
  		});
  	},
  	destroyProduct: function(product) {
  		// send an axios delete request to the backend to remove product from database
  		axios.delete("/api/products/" + product.id).then(response => {
  			console.log("Success!", response.data);
  			// find index of product in products array
  			var index = this.products.indexOf(product);
  			// splice products array at index
  			this.products.splice(index, 1);
  		});
  	}
  }
};
</script>
