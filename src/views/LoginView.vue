<template>
  <div class="login">
    <h1>Login</h1>
    <form @submit.prevent="login">
      <input type="text" id="username" v-model="username" placeholder="Username" required><br>
      <input type="password" id="password" v-model="password" placeholder="Password" required><br>
      <button type="submit">Login</button>
    </form>
    <p v-if="error" class="error">{{ error }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      error: ''
    };
  },
  methods: {
    login() {
      if (this.username === 'admin' && this.password === 'password') {
        localStorage.setItem('token', '12345'); 
        this.$router.push({ name: 'home' }); 
        this.error = ''; 
      } else {
        this.error = 'Invalid username or password. Please try again.';
      }
    }
  }
};
</script>
