<template>
  <div class="cart">
    <Navbar :updateCart="carts" />
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
              <li class="breadcrumb-item active" aria-current="page">Cart</li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col mt-3">
          <h4>My Cart</h4>
          <div class="table-responsive mt-3">
            <table class="table table-bordered">
              <thead class="bg-dark text-white">
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Product</th>
                  <th scope="col">Description</th>
                  <th scope="col">Qty</th>
                  <th scope="col">Price</th>
                  <th scope="col">Sub Total</th>
                  <th scope="col">Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(cart, index) in carts" :key="cart.id">
                  <th>{{ index + 1 }}</th>
                  <td>{{ cart.products.nama }}</td>
                  <td>{{ cart.description ? cart.description : "-" }}</td>
                  <td>{{ cart.qty }}</td>
                  <td>Rp. {{ cart.products.harga }}</td>
                  <td>
                    <strong>Rp. {{ cart.products.harga * cart.qty }}</strong>
                  </td>
                  <td align="center">
                    <button
                      class="btn btn-danger btn-sm"
                      @click="deleteCart(cart.id)"
                    >
                      <b-icon-trash-fill></b-icon-trash-fill> Delete
                    </button>
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right">
                    <strong>Grand Total</strong>
                  </td>
                  <td colspan="2" align="left">
                    <strong>Rp. {{ grandTotal }}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <div class="row justify-content-end mt-4">
        <div class="col-md-6">
          <form v-on:submit.prevent>
            <div class="form-group">
              <label for="full_name">Full Name</label>
              <input
                type="text"
                class="form-control"
                placeholder="Full Name"
                v-model="orders.full_name"
              />
            </div>
            <div class="form-group">
              <label for="phone_number">Phone Number</label>
              <input
                type="number"
                class="form-control"
                placeholder="Phone Number"
                min="0"
                v-model="orders.phone_number"
              />
            </div>
          </form>
          <button
            type="submit"
            class="btn btn-primary float-right"
            @click="checkout"
          >
            <b-icon-cart-fill></b-icon-cart-fill> Checkout
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
  name: "Cart",
  components: {
    Navbar,
  },
  data() {
    return {
      carts: [],
      orders: {},
    };
  },
  methods: {
    setCarts(data) {
      this.carts = data;
    },
    deleteCart(id) {
      axios
        .delete("http://localhost:3000/carts/" + id)
        .then(() => {
          this.$vToastify.success("Success Delete Cart Item");

          axios
            .get("http://localhost:3000/carts")
            .then((response) => this.setCarts(response.data))
            .catch((error) => console.log(error));
        })
        .catch((error) => console.log(error));
    },
    checkout() {
      if (this.orders.full_name && this.orders.phone_number) {
        this.orders.carts = this.carts;
        axios
          .post("http://localhost:3000/orders", this.orders)
          .then(() => {
            this.carts.map(function (items) {
              return axios
                .delete("http://localhost:3000/carts/" + items.id)
                .catch((error) => console.log(error));
            });
            this.$router.push("/checkout-success");
            this.$vToastify.success("Checkout Success");
          })
          .catch((err) => {
            console.log(err);
          });
      } else {
        this.$vToastify.error("Please fill all form");
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/carts")
      .then((response) => this.setCarts(response.data))
      .catch((error) => console.log(error));
  },
  computed: {
    grandTotal() {
      return this.carts.reduce(function (items, data) {
        return items + data.products.harga * data.qty;
      }, 0);
    },
  },
};
</script>

<style>
</style>