<template>
  <div>
      <h1>Products</h1>
      <div class="container">
        <div class="item" v-for="(product, index) in shop" :key="index">
          <h3>{{product.name}}</h3>
          <img :src="product.image">
          <p class="price">${{product.cost}}</p>
          <p><button @click="addItemToCart(product)">Add to Cart</button></p>
        </div>
      </div>
  </div>
</template>

<script>
export default {
    data() {
    return{
      page: "shop",
      cart: [],
      shop: [
        {
          id: 1,
          name: 'Apple',
          cost: 2.50,
          quantity:1,
          image: 'https://healthjade.com/wp-content/uploads/2017/10/apple-fruit.jpg'
        },
        {
          id: 2,
          name: 'Orange',
          cost: 2.99,
          quantity:1,
          image: 'https://i.redd.it/z60j3az3pos01.jpg'
        },
        {
          id: 3,
          name: 'Strawberry',
          cost: 3.50,
          quantity:1,
          image: 'https://bocabeacon.com/wordpress/wp-content/uploads/2017/02/strawberry.jpg'
        }
      ],
    };
  },

  methods: {
    addItemToCart(product) {
      this.$emit("addItemToCart", product);
    }
  }
}
</script>

<style scoped>
img {
  width: 200px;
  height: 200px;
  object-fit: contain;
}

.price {
  color: grey;
  font-size: 20px;
}

.item button {
  border: none;
  outline: 0;
  padding: 10px;
  color: white;
  background-color: rgb(93, 149, 223);
  text-align: center;
  cursor: pointer;
  font-size: 14px;
}

.item button:hover {
  opacity: 0.7;
}
.container {
  display: flex;
}

.item {
  flex-basis: 350px;
  height: 100px;
  margin: 50px;
}
</style>