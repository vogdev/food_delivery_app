<template>
  <div id="app">
    <Navbar v-on:SetComponent="SetComponent($event)" :propOrderCount='this.OrderCount' />
    <section class="section padding-top">
      <div class="container">
        <component  :is="this.Component" v-on:ShowComponent="ShowComponent($event)" v-on:AddToOrderCount="AddToOrderCount($event)" v-on:RemoveItemFromOrder="RemoveItemFromOrder($event)" :propProducts="this.Products" :propProduct="this.CurrentProduct" :propCustomerOrders="this.CustomerOrders" v-on:SetComponent="SetComponent($event)"></component>
      </div>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Index from '@/components/Index.vue'
import Show from '@/components/Show.vue'
import Cart from '@/components/Cart.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    // eslint-disable-next-line
    Index,
    // eslint-disable-next-line
    Show,
    // eslint-disable-next-line
    Cart
  },
  data: function () {
    // eslint-disable-next-line
    return{
      OrderCount: 0,
      Component: 'Index',
      // eslint-disable-next-line
      Products:[{"id":0, "title":"Pulled Chicken Tacos with Chili Salsa", "price":10, "currency":"$", "ingredients":["Chicken Breast", "Chili Salsa"], "img_url":"http://assets.kraftfoods.com/recipe_images/opendeploy/52514_640x428.jpg" ,"category":"", "description":"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos officiis voluptates, molestias et id corporis quos nulla, accusantium dignissimos quibusdam perferendis! Perferendis iure qui eligendi, in molestiae deserunt impedit consectetur."},{"id":1, "title":"Hamburger", "price":15, "currency":"$", "ingredients":["Ground beef", "Ground meat", "Macaroni"], "img_url":"https://www.thesun.co.uk/wp-content/uploads/2016/09/nintchdbpict000264481984.jpg?strip=all&w=800&h=800&crop=1" ,"category":"", "description":"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos officiis voluptates, molestias et id corporis quos nulla, accusantium dignissimos quibusdam perferendis! Perferendis iure qui eligendi, in molestiae deserunt impedit consectetur."},{"id":2, "title":"Clam chowder", "price":35, "currency":"$", "ingredients":["bacon strips", "butter", "celery ribs"], "img_url":"https://img.taste.com.au/tlo3N8xw/w720-h480-cfill-q80/taste/2016/11/prawn-potato-and-chorizo-chowder-108122-1.jpeg" ,"category":"", "description":"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos officiis voluptates, molestias et id corporis quos nulla, accusantium dignissimos quibusdam perferendis! Perferendis iure qui eligendi, in molestiae deserunt impedit consectetur."},{"id":3, "title":"Apple pie", "price":20, "currency":"$", "ingredients":["flour", "sugar", "salt"], "img_url":"https://www.landolakes.com/RecipeManagementSystem/media/Recipe-Media-Files/Recipes/Retail/x17/16800-blue-ribbon-apple-pie-760x580.jpg?ext=.jpg" ,"category":"", "description":"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos officiis voluptates, molestias et id corporis quos nulla, accusantium dignissimos quibusdam perferendis! Perferendis iure qui eligendi, in molestiae deserunt impedit consectetur."},{"id":4, "title":"Asiago Bagels", "price":25, "currency":"$", "ingredients":["flour", "brown sugar", "honey"], "img_url":"https://www.browneyedbaker.com/wp-content/uploads/2010/03/asiago-bagels2.jpg" ,"category":"", "description":"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos officiis voluptates, molestias et id corporis quos nulla, accusantium dignissimos quibusdam perferendis! Perferendis iure qui eligendi, in molestiae deserunt impedit consectetur."},{"id":5, "title":"Chicago-style pizza", "price":18, "currency":"$", "ingredients":["flour", "yellow cornmeal", "butter"], "img_url":"https://vitospizza.com/scottsdale/wp-content/uploads/2016/06/YY34811-min.jpg" ,"category":"", "description":"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos officiis voluptates, molestias et id corporis quos nulla, accusantium dignissimos quibusdam perferendis! Perferendis iure qui eligendi, in molestiae deserunt impedit consectetur."},{"id":6, "title":"Powder Biscuits", "price":5, "currency":"$", "ingredients":["flour", "butter", "milk"], "img_url":"https://d2gk7xgygi98cy.cloudfront.net/6163-3-large.jpg" ,"category":"", "description":"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos officiis voluptates, molestias et id corporis quos nulla, accusantium dignissimos quibusdam perferendis! Perferendis iure qui eligendi, in molestiae deserunt impedit consectetur."},{"id":7, "title":"Blueberry cobbler", "price":22, "currency":"$", "ingredients":["blueberries", "sugar", "flour"], "img_url":"https://upload.brickinc.net/recipe/2015/6/718776508.jpg" ,"category":"", "description":"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos officiis voluptates, molestias et id corporis quos nulla, accusantium dignissimos quibusdam perferendis! Perferendis iure qui eligendi, in molestiae deserunt impedit consectetur."}],
      CustomerOrders: [],
      CurrentProduct: {}
    }
  },
  mounted () {
    if (localStorage.getItem('OrderCount')) {
      this.OrderCount = JSON.parse(localStorage.getItem('OrderCount'))
    }
    if (localStorage.getItem('CustomerOrders')) {
      this.CustomerOrders = JSON.parse(localStorage.getItem('CustomerOrders'))
    }
    if (localStorage.getItem('Component')) {
      this.Component = JSON.parse(localStorage.getItem('Component'))
    }
    if (localStorage.getItem('CurrentProduct')) {
      this.CurrentProduct = JSON.parse(localStorage.getItem('CurrentProduct'))
    }
  },
  methods: {
    AddToOrderCount: function (product) {
      this.OrderCount += 1
      this.CustomerOrders.push(product)
    },
    RemoveItemFromOrder: function (product) {
      this.OrderCount -= 1
      let index = this.CustomerOrders.indexOf(product)
      this.CustomerOrders.splice(index, 1)
    },
    SetComponent: function (ComponentName) {
      this.Component = ComponentName
    },
    ShowComponent: function (product) {
      this.Component = 'Show'
      this.CurrentProduct = product
    }
  },
  watch: {
    OrderCount: {
      handler () {
        localStorage.setItem('OrderCount', JSON.stringify(this.OrderCount))
      }
    },
    CustomerOrders: {
      handler () {
        localStorage.setItem('CustomerOrders', JSON.stringify(this.CustomerOrders))
      }
    },
    Component: {
      handler () {
        localStorage.setItem('Component', JSON.stringify(this.Component))
      }
    },
    CurrentProduct: {
      handler () {
        localStorage.setItem('CurrentProduct', JSON.stringify(this.CurrentProduct))
      }
    }
  }
}
</script>
