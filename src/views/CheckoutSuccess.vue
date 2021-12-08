<template>
  <div class="checkout-success">
    <Navbar />
    <div class="container">
      <div class="row justify-content-center mt-4">
        <div class="text-center mt-4 mb-4">
          <img src="../assets/images/confirm.svg" width="300" style="margin-top: 50px; margin-bottom: 40px;" />
          <h4 class="mt-4"><strong>Thank you for your order.</strong></h4>
          <p style="margin-bottom: 70px;">
            Your order has been placed successfully. We will contact you soon.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  name: "CheckoutSuccess",
  components: {
    Navbar,
  },
};
</script>

<style>
</style>