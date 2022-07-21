<template>
  <div class="product-list">
<!--убрал функцию установки ширины карточки
    т.к. для этого достаточно css свойств-->
    <div class="card" v-for="product in products" :style="{width: cardsWidth + '%'}">
      <p class="card-title">{{ product.title }}</p>
      <img class="card-image" :src="product.image" alt="">
      <p class="card-price">Цена: {{ product.price }} {{ currency }}</p>
      <!--добавил форму и назвал ее свойством id тк. в ней можно обойтись
          без поиска перебирания всех рефов а сразу брать данные из нужной формы-->
      <div>
        <!-- ref нигде не используется но зачем то объявлен-->
        <input type="number" ref="amount" :id="product.id">
        <span>кг</span>
      </div>

      <button @click="addToCart(product)"> В корзину </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currency: String,
  },
  data() {
    return {
      //добавил переменную для записи в нее setInterval и еще одну в кол-вом миллисекунд - интервалом запроса к api
      products: [],
    };
  },
  computed: {
    cardsWidth() {
      <!--с этим прекрасно справятся css свойства-->
      let width = window.innerWidth;
      let count = 1;
      if (width > '840px') {
        count = 3;
      } else if ((width > '420px' && width < '840px')) {
        count = 2;
      }

      return 100 / count;
    },
  },
  methods: {
    //упростил функцию вызывая ее сразу в хуке created
    startPricesMonitoring() {
      setInterval(this.getList, 1000);
    },
    async getList() {
      let data = await this.$store.dispatch('getProductsList');

      this.products = data;
    },
    addToCart(product) {
      let amount = this.$refs.amount.find((input) => input.id === product.id).value;

      let data = {
        amount,
        price: product.price,
        title: product.title,
      };
      //убрал здесь отношения к родительскому компоненту $parent
      //чтобы сделать его более самостоятельным
      this.$parent.cart.push(data);
    },
  },
  created() {
    this.startPricesMonitoring();
  },
};
</script>

<style>
  .product-list {
    padding: 10px;
  }

  .card {
    display: inline-block;
    width: 100%;
    border: 1px solid #908888;
    border-radius: 5px;
    text-align: center;
    padding: 10px;
  }
  .card-image {
    width: 100%;
  }
  button {
    padding: 5px;
    margin: 5px;
  }

</style>
