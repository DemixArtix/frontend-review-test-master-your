<template>
  <div id="app">
    <!--убрал передачу всех props т.к. есть глоабльное хранилище,
    потому как здесь пока не наблюдается логики переиспользоваться
    где то еще компоненнты и передаваться другие данные в props-->
    <Header :cart="cart" :currency="currency"></Header>
    <List :currency="currency"/>
    <Cart :cart="cart"/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import List from './components/List.vue';
import Cart from './components/Cart.vue';

export default {
  //перенес корзину cart в store, чтобы сделать ее глобально доступной в любой точке приложения
  // и не привязывать к определенному компоненту, соответсвенно это делает приложение более легким для масштабирования
  name: 'App',
  data() {
    return {
      cart: [],
      currency: 'VGTB',
    };
  },
  components: {
    Header,
    List,
    Cart,
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
}
</style>
