<!--не соблюдается последовательность объявления основых тэгов vue компонента в таком же порядке как во всем приложении-->
<script>
export default {
  name: 'Header',
  props: {
    cart: Array,
    required: true,
    default: {},

    currency: String,
  },
  data() {
    return {
      cartPrice: 0,
    };
  },
  watch: {
    //перенес вычисления общей суммы товаров в store
    //и поменял на метод reduce и оставил два знака после запятой
    cart(cart) {
      let val = 0;
      cart.forEach((item) => {
        val += item.price * item.amount;
      });
      this.cartPrice = val;
    },
  },
}
</script>

<style scoped>
  .header {
    padding: 10px;
    background: #e5e5e5;
  }
</style>

<template>
  <div class="header">
    <h3>Товаров в корзине на: {{ cartPrice }} {{ currency }}</h3>
  </div>
</template>
