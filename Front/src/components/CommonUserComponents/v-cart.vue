<template>
  <div class="v-cart">
    <div class="container">
      <router-link :to="{ name: 'catalog' }">
        <keep-alive>
          <button class="my-3 btn btn-secondary round">
            Вернуться в каталог
          </button>
        </keep-alive>
      </router-link>
      <p v-if="!CART.length">Корзина пуста</p>
      <div class="row mt-3">
        <vCartItem
          v-for="(item, index) in CART"
          :key="item.article"
          :cart_item_data="item"
          @deleteFromCart="deleteFromCart(index)"
        ></vCartItem>
      </div>
      <div class="row text-start">
        <p v-if="CART.length">Сумма заказа: {{ SUM }}</p>
      </div>
    </div>
  </div>
</template>
<script>
import vCartItem from './v-cart-item.vue';
import { mapActions, mapGetters } from 'vuex';
export default {
  name: 'v-cart',
  props: {
    cart_data: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  methods: {
    ...mapActions(['DELETE_FROM_CART']),
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index);
    },
  },
  components: { vCartItem },
  data() {
    return {};
  },
  computed: {
    ...mapGetters(['CART', 'SUM']),
  },
};
</script>

<style></style>
