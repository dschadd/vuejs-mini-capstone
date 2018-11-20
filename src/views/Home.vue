<template>
  <div class="home">
    <div class="container">

      <div class="jumbotron">
        <h1 class="display-4">welcome to wild bear</h1>
        <p class="lead">food, stuff, and more</p>
        <hr class="my-4">
        <p>we sell some things here and we would like to sell them to you</p>
        <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a>
      </div>

      <h1>Add new product</h1>
      <button v-on:click="createRecipe()" class="btn btn-primary">Create new product</button>

      <div class="row">
        <div v-for="product in products" class="col-md-4 mb-2">
          <div class="card">
            <img class="card-img-top" v-bind:src="product.image_url" alt="Card image cap">
            <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">{{ product.description }}</p>
              <a href="#" class="btn btn-primary">get it</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
  
</style>

<script>
// @ is an alias to /src

var axios = require("axios");

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      products: []
    };
  },
  created: function() {
    axios.get("http://localhost:3000/api/products").then(
      function(response) {
        console.log(response.data);
        this.products = response.data;
      }.bind(this)
    );
  },
  methods: {
    createRecipe: function() {
      console.log("createRecipe");
      var params = {
        name: "dog",
        price: 2,
        description: "man's best friend",
        supplier_id: 2
      };
      axios.post("http://localhost:3000/api/products", params).then(
        function(response) {
          console.log(response);
          this.products.push(response.data);
        }.bind(this)
      );
    }
  },
  computed: {}
};
</script>
