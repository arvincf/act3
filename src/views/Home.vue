<template>
  <div id="home">
    <Shopping :cart="cart" @add-to-cart="addToCart" @remove-from-cart="removeFromCart" @navigate-to-login="navigateToLogin" />
  </div>
</template>

<script>
import Shopping from '@/components/CartView.vue';

export default {
  name: 'App',
  components: {
    Shopping
  },
  data() {
    return {
      cart: []
    };
  },
  methods: {
    addToCart(item) {
      const existingItem = this.cart.find(i => i.id === item.id);
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cart.push(item);
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    navigateToLogin() {
      this.$router.push({ name: 'login' });
    }
  }
};
</script>
