<template>
  <div class="home">
    <Navbar />
    <div class="container mt-3">
      <Hero />
      <div class="row mt-5">
        <div class="col">
          <h4>Best <strong>Products</strong></h4>
        </div>
        <div class="col">
          <router-link to="/products" class="btn btn-primary btn-sm float-right"
            ><b-icon-layers-fill></b-icon-layers-fill> View All</router-link
          >
        </div>
      </div>
      <div class="row mb-3 mt-3">
        <div class="col-md-4" v-for="product in products" :key="product.id">
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import Hero from "@/components/Hero.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Navbar,
    Hero,
    CardProduct,
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    setProduct(data) {
      this.products = data;
    },
  },
  mounted() {
    axios
      .get("https://my-json-server.typicode.com/fbiakbr/fbiakbr.github.io/best-products")
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error))
  },
};
</script>
