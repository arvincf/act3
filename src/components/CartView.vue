<template>
  <div class="Shopping">
    <h1>Add Product</h1><br>

    <form @submit.prevent="addNewProduct">
      <input type="text" id="productName" v-model="newProduct.name" placeholder="Product Name" required><br>
      <input type="number" id="productPrice" v-model.number="newProduct.price" min="0" step="0.01" placeholder="Price" required><br>
      
      <button type="submit">Add Product</button>
    </form>

    <h2>Product List:</h2>
    <div class="product-list">
      <div v-for="product in products" :key="product.id" class="product">
        <div v-if="product.id !== editingProductId">
          <p>{{ product.name }} [Price: ₱ {{ product.price }}]</p>
          <button @click="addToCart(product, product.quantityToAdd)">Add to Cart</button>
        </div>

        <div v-else class="edit-form">
          Product Name: <input type="text" v-model="editedProduct.name"><br>
          Price: <input type="number" v-model.number="editedProduct.price" min="1" step="0.01">
        </div>
      </div>
    </div>

    <h2>Cart:</h2>
    <div class="cart">
      <div v-for="(item, index) in cart" :key="index" class="cart-item">
        <button @click="addonCart(item)">+</button>
        <p>{{ item.name }} [₱{{ item.price }}] - Quantity: {{ item.quantity }}</p>
        <button @click="subtractToCart(item)">-</button><br>
        <button style="background-color: orange;" @click="removeFromCart(index)">Remove</button>
      </div>
      <p class="total">Total: ₱{{ totalPrice }}</p>
    </div>
    <button class="logout" @click="handleLogout">Logout</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { id: 1, name: 'Toyo', price: 109.50, quantityToAdd: 1 },
        { id: 2, name: 'Suka', price: 185, quantityToAdd: 1 },
        { id: 3, name: 'Patis', price: 500.76, quantityToAdd: 1 },
        { id: 4, name: 'Asukal', price: 225.05, quantityToAdd: 1 },
        { id: 5, name: 'Asin', price: 325.05, quantityToAdd: 1 },
        { id: 6, name: 'Paminta', price: 220.05, quantityToAdd: 1 }
      ],
      newProduct: {
        name: '',
        price: null
      },
      editingProductId: null,
      editedProduct: {
        id: null,
        name: '',
        price: null
      }
    };
  },
  watch: {
    products: {
      deep: true,
      handler(newProducts) {
        this.cart.forEach(cartItem => {
          const correspondingProduct = newProducts.find(product => product.id === cartItem.id);
          if (correspondingProduct) {
            cartItem.price = correspondingProduct.price;
          }
        });
      }
    }
  },
  props: ['cart', 'router'], 
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + (item.price * item.quantity), 0);
    }
  },
  methods: {
    addToCart(product, quantity) {
      const isAuthenticated = localStorage.getItem('token');
      if (isAuthenticated) {
        let existingItem = this.cart.find(item => item.id === product.id);
        if (existingItem) {
          existingItem.quantity += quantity;
        } else {
          this.$emit('add-to-cart', { id: product.id, name: product.name, price: product.price, quantity });
        }
      } else {
        this.$emit('navigate-to-login');
      }
    },
    removeProduct(id) {
      const index = this.products.findIndex(product => product.id === id);
      if (index !== -1) {
        this.products.splice(index, 1);
      }
    },
    removeFromCart(index) {
      this.$emit('remove-from-cart', index);
    },
    updateQuantity(index, quantity) {
      if (quantity < 1) {
        this.$emit('remove-from-cart', index);
      }
    },
    addonCart(item) {
      item.quantity++; // Increment quantity
      this.$emit('add-to-cart', item);
    },
    subtractToCart(item) {
      if (item.quantity > 1) {
        item.quantity--; // Decrement quantity only if it's greater than 1
        this.$emit('update-quantity', { item, quantity: item.quantity });
      }
    },
    addNewProduct() {
      if (this.newProduct.name && this.newProduct.price) {
        this.products.push({
          id: this.products.length + 1,
          name: this.newProduct.name,
          price: parseFloat(this.newProduct.price),
          quantityToAdd: 1
        });
        this.newProduct.name = '';
        this.newProduct.price = null;
      }
    },
    handleLogout() {
      localStorage.removeItem('token')
      this.$router.push('/login')
    }
  }
};
</script>
