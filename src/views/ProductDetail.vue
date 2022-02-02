<template>
  <div class="product-detail">
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/products">Products</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Product Order
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-4">
        <div class="col-md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            class="img-fluid shadow"
          />
        </div>
        <div class="col-md-6">
          <h4>{{ product.nama }}</h4>
          <hr />
          <h4>
            <strong>Rp. {{ product.harga }}</strong>
          </h4>
          <form v-on:submit.prevent>
            <div class="form-group">
              <label for="qty">Qty</label>
              <input
                type="number"
                class="form-control"
                min="1"
                placeholder="0"
                v-model="order.qty"
              />
            </div>
            <div class="form-group">
              <label for="description">Description</label>
              <textarea
                v-model="order.description"
                name="description"
                cols="30"
                rows="9"
                class="form-control"
                placeholder="Add Description"
              ></textarea>
            </div>
          </form>
          <button type="submit" class="btn btn-primary" @click="ordered">
            <b-icon-cart-fill></b-icon-cart-fill> Order Product
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "ProductDetail",
  components: {
    Navbar,
  },

  data() {
    return {
      product: {},
      order: {},
    };
  },

  methods: {
    setProduct(data) {
      this.product = data;
    },
    ordered() {
      if (this.order.qty) {
        this.order.products = this.product;
        axios
          .post("https://my-json-server.typicode.com/fbiakbr/fbiakbr.github.io/carts", this.order)
          .then(() => {
            this.$router.push("/cart");
            this.$vToastify.success("Added to Cart");
          })
          .catch((err) => {
            console.log(err);
          });
      } else {
        this.$vToastify.error("Qty is required");
      }
    },
  },

  mounted() {
    axios
      .get("https://my-json-server.typicode.com/fbiakbr/fbiakbr.github.io/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>