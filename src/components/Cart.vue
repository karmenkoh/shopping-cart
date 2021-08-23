<template>
        <h1>Cart</h1>
         <table class="table">
           <thead>
             <tr>
              <th>Product</th>
              <th></th>
              <th></th>
              <th>Price</th>
              <th>Quantity</th>
              <th></th>
              <th>Sub Total</th>
             </tr>
           </thead>
          <tbody>
            <tr v-for="(product,index) in cart" :key="index">
              <td colspan="2"><img :src="product.image" ></td>
              <td>{{product.name}}</td>
              <td>${{product.cost}}</td>
              <td>
                <input v-model="product.quantity" type="number" min="1"/>
              </td>
              
              <td><button @click="removeItemFromCart(product)">Remove</button></td>
              <td>${{product.cost * product.quantity}}</td>
            </tr>
          </tbody>
          <tfoot>
            <tr>
              <th colspan="5"></th>
              <td><strong><p>Total</p></strong></td>
              <td align="right"><strong><p>$ {{ total }}</p></strong></td>
            </tr>
          </tfoot>
        </table>
        
</template>

<script>
export default {
    props: ["cart"],

    computed: {
       total: function () {
          let total = 0;
          Object.values(this.cart).forEach(
          (product) => (total += parseFloat(product.cost) * parseFloat(product.quantity))
        );
        return total;
    },
  },

    methods: {
        removeItemFromCart(product){
            this.$emit("removeItemFromCart", product);
        }
}
}
</script>

<style scoped>
h1{text-align: center;}
table {
  border-collapse: collapse;
  width: 80%;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
}
th, td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}
tr:hover {background-color: rgb(238, 238, 238);}
td button{ 
  background-color: red;
  border: none;
  color: white;
  padding: 5px 15px;
  text-align: center;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  }
img {
  width: 150px;
  height: 150px;
  object-fit: contain;
}
</style>