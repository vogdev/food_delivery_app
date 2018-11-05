<template>
  <div class="home">
    <div class="cards">
      <h1 class="title" v-if="this.propCustomerOrders.length === 0" style="text-align: center;">Cart Empty</h1>
      <h1 class="title" v-if="this.propCustomerOrders.length !== 0" style="text-align: center;">Total: {{this.propCustomerOrders.map(x => x.price).reduce((a, b) => a + b, 0)}}$</h1>
      <div class="columns is-multiline">
        <div v-for="(product, index) in this.propCustomerOrders" :key="index" class="column is-6">
          <div class="card shadow-1">
            <div @click="fireShowComponent(product)" class="card-img-container">
              <img :src="product.img_url" :alt="product.title">
              <div class="price-container">
                <p>{{product.price}} {{product.currency}}</p>
              </div>
            </div>
            <div class="card-info">
              <p @click="fireShowComponent(product)" class="cart-card-title">{{product.title}}</p>
              <a @click="fireTheRemoveItemFromOrder(product)" class="remove-from-cart">-</a>
              <a @click="fireTheAddToOrder(product)" class="add-to-cart w-50">+</a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="ctas">
      <button class="add-item-btn button shadow-1" @click="fireSetComponent('Index')">Continue Shopping</button>
      <button :disabled="this.propCustomerOrders.length === 0" class="checkout-btn button shadow-1">Proceed to checkout</button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    propCustomerOrders: {
      type: Array
    }
  },
  // created: function () {
  //   // console.log(this.propCustomerOrders.map(x => x.price).reduce((a, b) => a + b, 0))
  // },
  methods: {
    fireTheAddToOrder: function (product) {
      this.$emit('AddToOrderCount', product)
    },
    fireShowComponent: function (product) {
      this.$emit('ShowComponent', product)
    },
    fireTheRemoveItemFromOrder: function (product) {
      this.$emit('RemoveItemFromOrder', product)
    },
    fireSetComponent: function (componentName) {
      this.$emit('SetComponent', componentName)
      if (this.showSideNav) {
        this.toggelSideNav()
      }
    }
  }
}
</script>

<style>
  .ctas{
    align-items: center;
    justify-content: center;
    width: 100%;
    margin-top: 70px;
    display: flex;
    flex-direction: column;
  }
  .cart-card-title {
    color: black;
    font-size: 16px;
    font-weight: 600;
    min-height: 40%;
    max-width: 80%;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    cursor: pointer;
  }
  .add-item-btn{
    width: 300px;
    background-color: white!important;
    border-color: #e4e4e4!important;
    font-size: 18px!important;
    font-weight: 600!important;
    border-radius: 100px!important;
  }
  .checkout-btn{
    color:black!important;
    border: 2px solid #000000!important;
    margin-top: 10px;
    width: 300px;
    background-color: #fff500!important;
    font-size: 18px!important;
    font-weight: 600!important;
    border-radius: 100px!important;
  }
  .remove-from-cart {
    background-color: #ff0000;
    border-color: #ffffff;
    border-width: 1px;
    color: #ffffff!important;
    font-size: 20px;
    font-weight: 700;
    position: absolute;
    top: -1px;
    right: -1px;
    width: 50px;
    cursor: pointer;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    padding-bottom: calc(0.375em - 1px);
    padding-left: 0.75em;
    padding-right: 0.75em;
    padding-top: calc(0.375em - 1px);
    text-align: center;
    white-space: nowrap;
    border-bottom-left-radius: 4px;
  }
  .w-50 {
    width: 50px;
  }
</style>
