<template>
  <div class="cart-list">
    <!--транслит -->
    <div v-for="item in spisok_dlya_rendera">
      <!--все данные отдаются объектом без вертски как есть. я вытащил свойства из объекта-->
      {{ item }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cart: Array,
  },
  computed: {
    //свойство которое возращает корзину в обратном порядке с помощью метода массива revese
    //я же в store добавил сразу добавление товаров в нужном порядке
    //плюс оно написано транслитом spisok-dlya-rendera я поменял на renderList
      spisok_dlya_rendera() {
          return this.cart.reverse();
      },
  },
};
</script>

<style>

</style>
