<template>
  <div id="app">
    <div>
      <product-list :products="products" @add-to-cart="addToCart"></product-list>
    </div>
    <div>
      <shopping-cart :cart="cart" @remove-from-cart="removeFromCart" @update-quantity="updateQuantity"></shopping-cart>
    </div>
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";
import ShoppingCart from "./components/ShoppingCart.vue";

export default {
  name: "App",
  components: {
    ProductList,
    ShoppingCart,
  },
  data() {
    return {
      products: [
        { id: 1, name: "Tote Bag", price: 20 },
        { id: 2, name: "Leather Bagpack", price: 50 },
        { id: 3, name: "Sling Bag", price: 30 },
      ],
      cart: [],
    };
  },
  methods: {
    addToCart(product) {
      const existingItemIndex = this.cart.findIndex(item => item.id === product.id);
      if (existingItemIndex !== -1) {
        this.cart[existingItemIndex].quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeFromCart(productId) {
      this.cart = this.cart.filter(item => item.id !== productId);
    },
    updateQuantity(payload) {
      const { productId, quantity } = payload;
      const cartItem = this.cart.find(item => item.id === productId);
      if (cartItem) {
        cartItem.quantity = quantity;
      }
    },
  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column; /* Ensure components stack vertically */
  align-items: center; /* Center components horizontally */
  padding: 30px;
}
</style>