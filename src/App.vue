<template>
  <div>
    <header>
      <button id="back" @click="navigateTo('shop')">Back</button>
      <button id="viewCart" v-on:click="navigateTo('cart')">View Cart</button>
      <div id="cartTotal">{{cart.length}} in cart</div>
      </header>

      <div v-if="page === 'cart'">
        <Cart v-on:removeItemFromCart="removeItemFromCart" :cart="cart"/>
      </div>
      
      <div v-if="page === 'shop'">
        <Product v-on:addItemToCart="addItemToCart"/>
      </div>
  </div>
</template>

<script>
import Product from './components/Product.vue';
import Cart from './components/Cart.vue';
export default {
  name: 'App',
  components: {Product, Cart},
 
  data() {
    return{
      page: "shop",
      cart: [],
    }
  },
methods: {
  addItemToCart(itemToAdd) {
      let found = false;

      // Add the item or increase qty
			let itemInCart = this.cart.find(product => product.id===itemToAdd.id);

      if (!itemInCart) {
        this.cart.push(itemToAdd);
      } else {
				itemInCart.quantity += itemToAdd.quantity;
			}
			
    },

  removeItemFromCart(product){
    this.cart.splice(this.cart.indexOf(product),1);
  },

  navigateTo(page) {
    this.page=page;
  }
}
}
</script>

<style scoped>
#back{
  background-color: grey;
  border: none;
  color: white;
  padding: 5px 15px;
  text-align: center;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
#viewCart{
  background-color: green;
  border: none;
  color: white;
  padding: 5px 15px;
  text-align: center;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  float: right;
}
#cartTotal{float: right;}

</style>
