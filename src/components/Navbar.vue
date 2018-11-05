<template>
<div class="navbar-container">
   <nav class="navbar navbar-fix" role="navigation" aria-label="main navigation">
     <div class="container">
      <div class="navbar-brand">
          <div @click="toggelSideNav" class="navbar-item">
            <svg height="32px" id="Layer_1" style="enable-background:new 0 0 32 32;" version="1.1" viewBox="0 0 32 32" width="32px" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><path d="M4,10h24c1.104,0,2-0.896,2-2s-0.896-2-2-2H4C2.896,6,2,6.896,2,8S2.896,10,4,10z M28,14H4c-1.104,0-2,0.896-2,2  s0.896,2,2,2h24c1.104,0,2-0.896,2-2S29.104,14,28,14z M28,22H4c-1.104,0-2,0.896-2,2s0.896,2,2,2h24c1.104,0,2-0.896,2-2  S29.104,22,28,22z"/></svg>
          </div>
          <div class="navbar-item" @click="fireSetComponent('Index')">
            <h1 class="logo">FoodAPP</h1>
          </div>
          <div @click="fireSetComponent('Cart')" class="navbar-item">
            <div class="badge" v-if="this.propOrderCount > 0"><p>{{this.propOrderCount}}</p></div>
            <svg width="28" style="enable-background:new 0 0 24 24;" version="1.1" viewBox="0 0 24 24" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><g id="info"/><g id="icons"><g id="cart"><path d="M20,13H4c-0.7,0-1.1,0.6-1,1.2l1.4,6.2c0.2,0.9,1,1.6,2,1.6h11.1c1,0,1.8-0.7,2-1.6l1.4-6.2C21.1,13.6,20.6,13,20,13z     M11,18c0,0.5-0.4,1-1,1s-1-0.5-1-1v-2c0-0.5,0.4-1,1-1s1,0.5,1,1V18z M15,18c0,0.5-0.4,1-1,1s-1-0.5-1-1v-2c0-0.5,0.4-1,1-1    s1,0.5,1,1V18z"/><path d="M21,8h-2.2l-1.9-4.8c-0.4-1-1.6-1.5-2.6-1.1c-1,0.4-1.5,1.6-1.1,2.6L14.5,8H9.5l1.3-3.3c0.4-1-0.1-2.2-1.1-2.6    c-1-0.4-2.2,0.1-2.6,1.1L5.2,8H3c-1.1,0-2,0.9-2,2v1c0,0.6,0.4,1,1,1h20c0.6,0,1-0.4,1-1v-1C23,8.9,22.1,8,21,8z"/></g></g></svg>
          </div>
        </div>
      </div>
    </nav>
    <aside :class="showSideNav?'show-side-nav':''" class="menu">
      <ul class="menu-list">
        <li><a @click="fireSetComponent('Index')">Home</a></li>
        <li><a @click="fireSetComponent('Cart')">Cart</a></li>
      </ul>
    </aside>
    <div @click="toggelSideNav" :class="showBlackBg? 'show-black-bg': ''" class="black-bg"></div>
</div>
</template>

<script>
export default {
  name: 'Navbar',
  props: {
    propOrderCount: Number
  },
  data: function () {
    // eslint-disable-next-line
    return{
      showBlackBg: false,
      showSideNav: false
    }
  },
  methods: {
    fireSetComponent: function (componentName) {
      this.$emit('SetComponent', componentName)
      if (this.showSideNav) {
        this.toggelSideNav()
      }
    },
    toggelSideNav: function () {
      this.showBlackBg = !this.showBlackBg
      this.showSideNav = !this.showSideNav
      document.getElementsByTagName('html')[0].classList.toggle('is-clipped')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.navbar {
  background-color: #fff500;
  min-height: 3.25rem;
  position: relative;
  z-index: 30;
}
.logo {
  font-weight: 600;
  color: black;
  font-size: 27px;
  line-height: normal;
  cursor: pointer;
}
.navbar-brand, .navbar-tabs {
  display: flex;
  align-items: center;
  justify-content: space-between;
  min-height: 3.8rem;
  width: 100%;
}
.badge {
  position: absolute;
  top: -2px;
  right: 3px;
  width: 25px;
  height: 25px;
  border-radius: 25px;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  user-select: none;
}
.badge p{
  color: black!important;
  line-height: 1;
  text-align: center;
  font-weight: 700;
}
aside {
  transition: all 0.2s ease-out;
  position: fixed;
  top: 60px;
  bottom: 0;
  z-index: 900;
  background-color: #ffffff;
  left: -350px;
  padding: 10px 0px 0px 10px;
  width: 250px;
}
aside li {
  text-align: center;
}
.black-bg {
  transition: all 0.2s ease-out;
  position: fixed;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.61);
  z-index: 890;
  opacity: 0;
  display: none;
}
.show-black-bg {
  transition: all 0.2s ease-out;
  opacity: 1;
  display: block;
}
.show-side-nav {
  transition: all 0.2s ease-out;
  left: 0;
}
.navbar-fix {
  position: fixed;
  width: 100%;
  top: -1px;
  z-index: 990;
}
</style>
