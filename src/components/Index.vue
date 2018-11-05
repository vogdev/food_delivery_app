<template>
  <div class="home">
    <div class="main-card shadow-1">
      <img src="../assets/img/main.png" alt="">
      <div class="main-card-info">
        <div class="main-info">
          <p class="main-card-title">Hamburger Steak with Onions</p>
          <p class="main-price">40 $</p>
        </div>
      </div>
    </div>
    <div class="cards">
      <div class="columns is-multiline">
        <div v-for="(product, index) in this.propProducts" :key="index" class="column is-6">
          <div class="card shadow-1">
            <div @click="fireShowComponent(product)" class="card-img-container">
              <img :src="product.img_url" :alt="product.title">
              <div class="price-container">
                <p>{{product.price}} {{product.currency}}</p>
              </div>
            </div>
            <div class="card-info">
              <p @click="fireShowComponent(product)" class="card-title">{{product.title}}</p>
              <p class="card-additional-info">{{product.ingredients.join()}}</p>
              <a @click="fireTheAddToOrder(product)" class="add-to-cart">Add</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    propProducts: {
      type: Array
    }
  },
  methods: {
    fireTheAddToOrder: function (product) {
      this.$emit('AddToOrderCount', product)
    },
    fireShowComponent: function (product) {
      this.$emit('ShowComponent', product)
    }
  }
}
</script>

<style>
  .main-card {
    height: 240px;
    position: relative;
    border-radius: 4px;
    overflow: hidden;
  }
  .main-card img{
    object-fit: cover;
    height: 100%;
    width: 100%;
  }
  .main-card-info{
    position: absolute;
    height: 50%;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    background-image: linear-gradient(rgba(255, 255, 255, 0), rgba(0, 0, 0, 0.81));
  }
  .main-info {
    width: 100%;
    max-height: 150px;
    position: absolute;
    bottom: 0;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    padding: 10px;
  }
  .main-price {
    color: #fff500;
    font-size: 30px;
    font-weight: 500;
  }
  .main-card-title{
    color: #FFF;
    font-size: 20px;
    font-weight: 600;
    max-width: 70%;
  }
  .card{
    margin-top: 20px;
    height: 130px;
    display: flex;
    border-radius: 4px;
    overflow: hidden;
  }
 .card-img-container {
    min-width: 150px;
    height: 130px;
    background-color: black;
    position: relative;
    cursor: pointer;
  }
  .card-info {
    padding: 5px;
    position: relative;
    width: 100%;
    height: 100%;
  }
  .card-img-container img{
    width: 150px;
    height: 130px;
    object-fit: cover;
  }
  .price-container {
    position: absolute;
    bottom: 0;
    height: 60%;
    width: 100%;
    background-image: linear-gradient(rgba(255, 255, 255, 0), rgba(0, 0, 0, 0.75));
  }
  .price-container p{
    position: absolute;
    bottom: 0;
    right: 0;
    color: #fff500;
    font-size: 25px;
    font-weight: 500;
    padding-right: 5px;
  }
  .card-title{
    color: black;
    font-size: 16px;
    font-weight: 600;
    min-height: 20%;
    display: flex;
    align-items: center;
    cursor: pointer;
  }
  .card-additional-info{
    color: #a1a1a1;
  }
  .add-to-cart {
    background-color: #fff500;
    border-color: #ffffff;
    border-width: 1px;
    color: #000000!important;
    font-size: 20px;
    font-weight: 700;
    position: absolute;
    bottom: -1px;
    right: -1px;
    width: 100px;
    cursor: pointer;
    -webkit-box-pack: center;
    justify-content: center;
    padding-bottom: calc(0.375em - 1px);
    padding-left: 0.75em;
    padding-right: 0.75em;
    padding-top: calc(0.375em - 1px);
    text-align: center;
    white-space: nowrap;
    border-top-left-radius: 4px;
  }
  .cards {
    margin-top: 10px;
  }
  @media only screen and (max-width: 769px) {
    .cards {
      margin-top: 0px;
    }
  }
</style>
