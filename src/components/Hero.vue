<template>
  <div class="row">
      <div class="col-6">
          <div class="d-flex h-100">
              <div class="justify-content-ceter align-self-center">
                  <h2><strong>Spend less. Smile more.</strong></h2>
                  <p>Free shipping on millions of items.<br>Get the best of Shopping and Entertainment with  <strong>Naruhodo.</strong></p>
                  <router-link class="btn btn-block btn-primary" to="/products">
                    <b-icon icon="cart-check-fill"></b-icon>
                    Start Shopping Now
                  </router-link>
              </div>
          </div>
      </div>
      <div class="col-6">
          <img src="../assets/images/deliv.svg" class="ml-5" width="470px">
      </div>
  </div>
</template>

<script>
export default {
    name: 'Hero',
}
</script>

<style>

</style>