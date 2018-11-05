<template>
  <div class="home">
    <div class="show-main-card shadow-1">
      <img  class="show-img" :src="this.propProduct.img_url" :alt="this.propProduct.title">
      <div class="main-card-info">
        <div class="main-info">
          <p class="main-card-title">{{this.propProduct.title}}</p>
          <p class="main-price">{{this.propProduct.price}} {{this.propProduct.currency}}</p>
        </div>
      </div>
    </div>
    <div class="show-info-cart shadow-1">
      <h1 class="show-info-cart-heading">Ingredients:</h1>
      <p class="card-additional-info">{{this.propProduct.ingredients.join(" | ")}}</p>
      <h1 class="show-info-cart-heading">Description:</h1>
      <p>{{this.propProduct.description}}</p>
    </div>
    <div class="show-add-to-cart">
      <button @click="fireTheAddToOrder()" class="checkout-btn button shadow-1">ADD to cart</button>
    </div>
    <div class="recommended">

    </div>
  </div>
</template>
<script>
export default {
  props: {
    propProduct: {
      type: Object
    }
  },
  methods: {
    fireTheAddToOrder: function () {
      this.$emit('AddToOrderCount', this.propProduct)
    }
  }
}
</script>

<style>
.show-add-to-cart {
  text-align: center;
}
.show-main-card {
  height: 300px;
  position: relative;
  border-radius: 4px;
  overflow: hidden;
}
.show-img {
  height: 100%;
  width: 100%;
  object-fit: cover;
}
.show-info-cart {
  background-color: white;
  margin-top: 20px;
  border-radius: 4px;
  overflow: hidden;
  padding: 10px;
}
.show-info-cart-heading{
  color: #000;
  font-size: 20px;
  font-weight: 600;
  margin: 10px 0px;
}
</style>
