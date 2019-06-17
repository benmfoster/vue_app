<template>
  <div class="products-show">
   <h2>{{ product.name }}</h2>
   <p>Description: {{ product.description }}</p>   
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      product: {}
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id).then(response => {
      this.product = response.data;
      console.log(this.product);
    });
  },
  methods: {
  }
};
</script>