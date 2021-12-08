<template>
  <div class="card shadow card-product mb-4">
    <img :src=" 'assets/images/' + product.gambar" class="card-img-top" />
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <p class="card-text">
        <strong>
        Rp. {{ product.harga }}
        </strong>
      </p>
      <router-link :to="'/products/'+product.id" class="btn btn-primary btn-block btn-md"><b-icon-cart-fill></b-icon-cart-fill> Buy Now</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script>

<style>
</style>