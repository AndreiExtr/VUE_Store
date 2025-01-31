<template>
  <div class="card" :class="{ 'card--sold': showText }">
    <div class="card__img">
      <img :src="imageSrc" :alt="title">
    </div>
    <div class="card__content">
      <h2>{{ title }}</h2>
      <div class="price-bt">
        <div class="prices" v-if="showPrice">
          <p v-if="oldPrice" style="text-decoration: line-through;color: #A0A0A0;font-size: 14px;font-weight: 300;">
            {{ oldPrice }} $
          </p>
          <p>{{ newPrice }} $</p>
        </div>
        <p v-if="showText"> Продана на аукционе </p>
        <ButtonUI
          v-if="!showText"
          :show-icon="isInCart"
          :is-in-cart="isInCart"
          :label="buttonLabel"
          :is-processing="isProcessing"
          @click.stop="toggleCart"/>
      </div>
    </div>
  </div>
</template>

<script>
import ButtonUI from './ButtonUI.vue'
import { ref, computed, onMounted } from 'vue'

export default {
  name: 'CardUI',
  components: {
    ButtonUI
  },
  props: {
    image: String,
    title: String,
    oldPrice: [String, Number],
    newPrice: [String, Number],
    showText: {
      type: Boolean,
      default: false
    },
    showPrice: {
      type: Boolean,
      default: false
    }
  },
  emits: ['update-cart'],
  setup (props, { emit }) {
    const isInCart = ref(false)
    const isProcessing = ref(false)

    // Загрузка состояние корзины
    const loadCartState = () => {
      const cartItems = JSON.parse(localStorage.getItem('cart')) || []
      isInCart.value = cartItems.includes(props.title)
    }

    // Добавляется/удаляется товар из корзины
    const toggleCart = async () => {
      if (isInCart.value || isProcessing.value) return // Если в корзине или процесс добавления

      isProcessing.value = true

      // Имитация асинхронной операции (добавление в корзину)
      await new Promise(resolve => setTimeout(resolve, 2000))

      const cartItems = JSON.parse(localStorage.getItem('cart')) || []
      if (!cartItems.includes(props.title)) {
        cartItems.push(props.title)
        localStorage.setItem('cart', JSON.stringify(cartItems))
      }

      isInCart.value = true
      isProcessing.value = false

      emit('update-cart', props.title, true)
    }

    onMounted(loadCartState)

    return {
      isInCart,
      isProcessing,
      buttonLabel: computed(() => (isInCart.value ? 'В корзине' : 'Купить')),
      toggleCart
    }
  },
  computed: {
    imageSrc () {
      return require(`@/assets/${this.image}`)
    }
  }
}
</script>

<style lang="scss">
.card--sold {
  opacity: 0.5;
  pointer-events: none;
}
.card{
  width: 280px;
  height: 328px;
  border: 1px solid #E1E1E1;
  transition: box-shadow 0.3s ease-in-out, transform 0.3s ease-in-out;

  @media (max-width: 1280px) {
    height: 400px;
  }

  @media (max-width: 992px) {
    width: 100%;
  }

  &:hover{
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    transform: translateY(-2px);
    cursor: pointer;
  }

  &__img{
    height: 160px;
    border-bottom: 1px solid #E1E1E1;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }

  &__content{
    height: 168px;
    padding: 24px;
    font-size: 18px;
    line-height: 150%;
    text-align: left;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    @media (max-width: 1280px) {
      height: 240px;
      padding: 16px;
    }

    h2{
      color: #343030;
    }

    .price-bt{
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;

      @media (max-width: 1280px) {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 12px;
      }

      .prices{
        display: flex;
        flex-direction: column;
      }

      p{
        font-size: 16px;
        font-weight: 700;
        color: #343030;
      }
    }
  }
}
</style>
