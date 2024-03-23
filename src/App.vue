<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/login">Login</router-link>
  </nav>
  <router-view/>
</template>

<style>
/* App.vue */
#app {
  font-family: 'Arial', sans-serif;
}

/* Navigation */
nav {
  padding: 20px;
  text-align: center;
  background-color: #333;
}

nav a {
  font-weight: bold;
  color: #fff;
  text-decoration: none;
  margin: 0 10px;
}

nav a.router-link-exact-active {
  color: #42b983;
  background-color: #fff;
  border-radius: 5px;
  padding: 5px 10px;
}

/* Shopping Component */
.Shopping {
  margin: 20px auto;
  max-width: 600px;
}

.product-list {
  margin-top: 20px;
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* Three columns */
  grid-gap: 20px; /* Spacing between products */
}

.product {
  border: 1px solid #ccc;
  padding: 10px;
}

.product p {
  margin: 0; /* Remove default margin */
}


.edit-form input[type="text-edit"],
.edit-form input[type="number"] {
  width: 100%;
  margin-bottom: 10px;
  padding: 5px;
}

.edit-form button {
  background-color: #42b983;
  color: #fff;
  border: none;
  padding: 5px 10px;
  margin-top: 10px;
  cursor: pointer;
  display: block;
  margin: 0 auto; /* Center aligns the button horizontally */
}

.cart-item button {
  background-color: #ff6347;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  display: block;
  margin: 0 auto; /* Center aligns the button horizontally */
}

.cart {
  margin-top: 20px;
  border: 1px solid #ccc;
  padding: 10px;
}

.cart-item {
  border-bottom: 1px solid #ccc;
  padding: 10px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.cart-item input[type="number"] {
  width: 50px;
}

.cart-item button {
  background-color: #ff6347;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

.total {
  margin-top: 10px;
  font-weight: bold;
}

/* Login Component */
.login {
  max-width: 300px;
  margin: 20px auto;
}

.login h1 {
  text-align: center;
  margin-bottom: 20px;
}

.login input {
  width: 100%;
  margin-bottom: 10px;
  padding: 8px;
}

.login button {
  width: fit-content;
  background-color: #42b983;
  color: #fff;
  padding: 10px;
  cursor: pointer;
  display: block;
  margin: 0 auto; /* Center aligns the button horizontally */
}

.login .error {
  color: #ff6347;
  margin-top: 10px;
  text-align: center;
}

/* Logout Button */
.logout {
  color: white;
  background-color: red;
  text-align: center;
  display: block;
  margin: 0 auto; 
  width: fit-content; 
}

/* Home Component */
#home {
  padding: 20px;
}

/* Form Input Styles */
input[type="text"],
input[type="password"],
input[type="number"] {
  width: 100%;
  margin-bottom: 10px;
  padding: 8px;
}

button {
  background-color: #42b983;
  color: #fff;
  border: none;
  padding: 10px;
  cursor: pointer;
}

button[type="submit"] {
  width: 100%;
}
</style>
