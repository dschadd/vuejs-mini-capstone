<template>
  <div class="home">
    <div class="container">
      <div class="jumbotron">
        <h1 class="display-4">welcome to wild bear</h1>
        <p class="lead">food, stuff, and more</p>
        <hr class="my-4" />
        <p>we sell some things here and we would like to sell them to you</p>
        <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a>
      </div>
      
      <ul>
        <li v-for="error in errors" class="text-danger">{{error}}</li>
      </ul>
      <h1>Add new product</h1>
      Name <input v-model="newProductName" type="text" /> Price
      <input v-model="newProductPrice" type="text" /> Description
      <input v-model="newProductDescription" type="text" /> Supplier_ID
      <input v-model="newProductSupplierID" type="text" />
      <button v-on:click="createProduct();" class="btn btn-primary"> Create new product </button>

      <h1>Search Products</h1>
      <input type="text" v-model="searchFilter" list="names">
      <datalist id="names">
        <option v-for="recipe in recipes">{{ recipe.title }}</option>
      </datalist>
      <div class="row">
        <div v-for="product in filterBy(products, searchFilter, 'name', 'description')" class="col-md-4 mb-2">
          <div class="card">
            <img
              class="card-img-top"
              v-bind:src="product.images[0].image_url"
              alt="Card image cap"
            />
            <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">{{ product.description }}</p>
              <a v-bind:href="`/#/products/${product.id}`" class="btn btn-primary">get it</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
// @ is an alias to /src

var axios = require("axios");

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      products: [],
      newProductName: "",
      newProductPrice: "",
      newProductDescription: "",
      newProductSupplierID: "",
      searchFilter: ""
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
    createProduct: function() {
      console.log("createProduct");
      var params = {
        name: this.newProductName,
        price: this.newProductPrice,
        description: this.newProductDescription,
        supplier_id: this.newProductSupplierID
      };
      axios.post("http://localhost:3000/api/products", params).then(
        function(response) {
          console.log(response);
          this.products.push(response.data);
          this.newProductName = "";
          this.newProductPrice = "";
          this.newProductDescription = "";
          this.newProductSupplierID = "";
        }.bind(this)
      );
    }
  },
  computed: {}
};
</script>
