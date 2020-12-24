<template>
  <div class="container">
    <div class="sidebar">
      <div class="title">
        <h2>My Order</h2>
        <p>Take Out</p>
      </div>
      <ul v-if="orders != ''" >
        <li v-for="order in orders" :key="order.id">
          <Cardlt v-bind:somme="total" :order="order" :name="order.name" :price="order.price" :count="order.count" :link='order.url' @addTo="addTo($event)" @supTo="supTo($event)"/>
        </li>
      </ul>
      <div class="total">
        <p>Total</p>
        <h2>${{ total }}</h2>
        <button class="btn-total">Done</button>
      </div>
    </div>
    <section>

      <img class="logo" src="../assets/mcdonalds.svg" alt="">

      <h1 class="whatsup"><span class="hey">Hey,</span><br>
      what's up?</h1>
      <div class="menu-wrapper">
        <Menu v-for="item in items" :key="item.id" :item="item" :name="item.name" :url='item.url'  @add="addItem($event)"/>
      </div>

      <h1 class="popular">Popular</h1>
      <div class="menu-wrapper">
        <Menu v-for="pop in populars" :key="pop.id" :item="pop" :name="pop.name" :url='pop.url'  @add="addItem($event)"/>
      </div>
    </section>
  </div>
</template>

<script>

export default {
  data () {
    return {
      orders: [],
      total: 0,
      items: [
        {name: 'pizza', price: 9, count: 1, url:require(`~/assets/pizza.svg`) },
        {name: 'burger', price: 6, count: 1, url:require(`~/assets/burger.svg`)},
        {name: 'cheese-burger', price: 7, count: 1, url:require(`~/assets/cheese-burger.svg`)},
        {name: 'burrito', price: 4, count: 1, url:require(`~/assets/burrito.svg`)},
        {name: 'hot dog', price: 7, count: 1, url:require(`~/assets/hot-dog.svg`)},
        {name: 'chicken', price: 7, count: 1, url:require(`~/assets/roast-chicken.svg`)},
      ],
      populars: [
        {name: 'birthday cake', price: 12, count: 1, url:require(`~/assets/birthday-cake.svg`)},
        {name: 'chicken leg x5', price: 5, count: 1, url:require(`~/assets/chicken-leg.svg`)},
        {name: 'french fries', price: 3, count: 1, url:require(`~/assets/french-fries.svg`)},
        {name: 'sandwich', price: 3, count: 1, url:require(`~/assets/sandwich.svg`)},
        {name: 'bell pepper', price: 8, count: 1, url:require(`~/assets/bell-pepper.svg`)},
      ]
    }
  },
  head(){
    title: 'Wcdonalds'
  },
  methods: {
    addTo(addEvent){
      this.total += addEvent.price
      addEvent.count ++
    },
    supTo(supEvent){
      if (supEvent.count === 1) {
        this.total -= supEvent.price
        this.orders.splice(this.orders.indexOf(supEvent),1)
      } else {
        this.total -= supEvent.price
        supEvent.count --
      }
    },
    addItem(item){
      this.total += item.price
      this.orders.push(item)
    },
  }
}
</script>

<style>
  body{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  .container{
    height: 700px;
    width: 400px;
    background-color: white;
    border-radius: 50px;
    border: 5px solid black;
    display: flex;
    flex-direction: row-reverse;
    padding-left: 26px;
  }

  .popular{
    margin-left: 10px;
    font-weight: bolder;
  }

  .hey{
    font-weight: bolder;
  }

  .whatsup{
    margin: 50px 0 20px 10px;
  }

  section{
    width: 70%;
    overflow: scroll;
    -ms-overflow-style: none;
    overflow: -moz-scrollbars-none; 
  }

  section::-webkit-scrollbar{
    display: none;
  }

  .logo{
    height: 40px;
    transform: rotate(180deg);
    margin: 20px 0 0 20px;
    cursor: pointer;
  }

  .sidebar{
    height: 100%;
    width: 30%;
    background-color: #F8F8F8;
    border-radius: 0 50px 50px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
  }

  .sidebar ul{
    list-style: none;
    width: 100%;
    overflow: scroll;
  }

  .sidebar p{
    color: #D2D2D2;
    font-size: .7rem;
    font-weight: 600;
  }

  .title{
    margin-top: 100px;
  }

  .total{
    margin-bottom: 50px;
    display: flex;
    flex-direction: column;
    align-items: center;
    border-top: 1px solid #EBEBEB;
    padding-top: 20px;
  }

  .total h2{
    margin-bottom: 10px;
  }

  .btn-total{
    height: 80px;
    width: 80px;
    border-radius: 30%;
    border: none;
    background: #FFC100;
    cursor: pointer;
    outline: none;
    font-weight: bold;
  }

  .card-lt{
    border-top: 1px solid #EBEBEB;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-left: -30px;
    margin-top: 20px;
    padding-top: 20px;
  }

  .card-lt img{
    height: 30px;
  }

  .btn-card-lt{
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 100%;
  }

  .btn{
    cursor: pointer;
    height: 15px;
    width: 30px;
    border-radius: 30px;
    border: none;
    display: flex;
    align-items: center;
    justify-content: center;
    outline: none;
  }

  .btn-plus{
    background-color: #FFC100;
  }

  .btn-minus{
    background-color: transparent;
    border: 1px solid #D2D2D2;
  }

  .menu-wrapper{
    display: flex;
    flex-wrap: wrap;
  }

</style>
