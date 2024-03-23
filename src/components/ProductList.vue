<template>
    <div>
      <h2 class="center">Products</h2>
      <ul class="product-list">
        <li v-for="product in products" :key="product.id" class="product-item">
          <div>{{ product.name }}</div>
          <div>₱{{ product.price }}</div>
          <button class="add-to-cart-btn" @click="addToCart(product)">Add to Cart</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      products: {
        type: Array,
        required: true,
      },
    },
    methods: {
      addToCart(product) {
        this.$emit("add-to-cart", product);
      },
    },
  };
  </script>
  
  <style scoped>
  .center {
    text-align: center;
  }
  
  .product-list {
    list-style: none;
    padding: 0;
  }
  
  .product-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  .add-to-cart-btn {
    background-color: #ffa500; /* light orange */
    border: none;
    color: white;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
  }
  </style>
  