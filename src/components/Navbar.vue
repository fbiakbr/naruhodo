<template>
  <nav class="navbar navbar-expand-lg navbar-light">
    <div class="container">
      <a class="navbar-brand" href="">Naruhodo</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/products">Products</router-link>
          </li>
        </ul>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/cart">
              Shopping Cart
              <b-icon-cart></b-icon-cart>
              <span class="badge badge-primary ml-1">{{ updateCart ? updateCart.length : qtys.length }}</span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from 'axios';

export default {
  name: "Navbar",
  data() {
    return {
      qtys: []
    };
  },
  props: ['updateCart'],
  methods: {
    setQtys(data) {
      this.qtys = data;
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/carts")
      .then((response) => this.setQtys(response.data))
      .catch((error) => console.log(error))
  }
};
</script>

<style>
</style>