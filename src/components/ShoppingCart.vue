<template>
    <div>
      <h2 class="center">Shopping Cart</h2>
      <ul class="cart-list">
        <li v-for="item in cart" :key="item.id" class="cart-item">
          <div>{{ item.name }}</div>
          <div>
            ₱{{ item.price }} – Quantity:
            <input type="number" v-model="item.quantity" @change="updateQuantity(item.id, item.quantity)">
          </div>
          <button class="remove-from-cart-btn" @click="removeFromCart(item.id)">Remove</button>
        </li>
      </ul>
      <div class="total">Total: ₱{{ totalPrice }}</div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cart: {
        type: Array,
        required: true,
      },
    },
    computed: {
      totalPrice() {
        return this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
      },
    },
    methods: {
      removeFromCart(productId) {
        this.$emit("remove-from-cart", productId);
      },
      updateQuantity(productId, quantity) {
        this.$emit("update-quantity", { productId, quantity: parseInt(quantity) });
      },
    },
  };
  </script>
  
  <style scoped>
  .center {
    text-align: center;
  }
  
  .cart-list {
    list-style: none;
    padding: 0;
  }
  
  .cart-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  .remove-from-cart-btn {
    background-color: #ffa500; /* light orange */
    border: none;
    color: white;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .total {
    text-align: center;
    margin-top: 10px;
  }
  </style>
  