<template>
  <div class="products-new">

    <h1>New Product</h1>

    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
      <div class="form-row">
        <div class="form-group col-md-6">
          <label for="name">Name</label>
          <input type="text" class="form-control" id="name" placeholder="Product Name" v-model="newProductName" />
        </div>
        <div class="form-group col-md-6">
          <label for="description">Description</label>
          <input type="number" class="form-control" id="description" placeholder="Various various attributes of the product, including secrete powers, price, smell, etc." v-model="newProductDescription">
        </div>
      </div>
      <button type="submit" class="btn btn-success">Create</button>
    </form>    
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      newProductName: "",
      newProductDescription: "",
      errors: []
    };
  },
  created: function() {
  },
  methods: {
  	createProduct: function() {
  		// make a post request via axios to create a new product in our database!
  		var params = {
  			name: this.newProductName,
  			description: this.newProductDescription
  		};
  		axios.post("/api/products", params).then(response => {
  			this.$router.push("/");
  		}).catch(error => {
        this.errors = error.response.data.errors;
      });
  	}
  }
};
</script>