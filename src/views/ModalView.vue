<template>
  <div v-if="isVisible" class="modal-overlay" @click="closeModal">
    <div class="modal-content" @click.stop>
      <button class="close-btn" @click="closeModal">X</button>
      <div class="slider">
        <button @click="prevImage" class="slider-btn prev-btn" v-if="images && images.length > 1">←</button>
        <img v-if="images && images.length > 0" :src="currentImage" alt="Painting Image" class="slider-image" />
        <button @click="nextImage" class="slider-btn next-btn" v-if="images && images.length > 1">→</button>
      </div>
      <div class="slider-content">
        <h2>{{ title }}</h2>
        <p>{{ description }}</p>
        <div class="prices">
          <span class="new-price">Стоимость: {{ newPrice }} $</span>
          <span v-if="oldPrice" class="old-price">{{ oldPrice }} $</span>
        </div>
      </div>
      <ButtonUI
        :show-icon="isInCart"
        :is-in-cart="isInCart"
        :label="buttonLabel"
        :is-processing="isProcessing"
        @click="toggleCart"/>
    </div>
  </div>
</template>

<script>
import ButtonUI from '@/components/elements/ButtonUI.vue'
import { ref, computed, onMounted } from 'vue'

export default {
  name: 'PaintingModal',
  components: {
    ButtonUI
  },
  props: {
    isVisible: {
      type: Boolean,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    images: {
      type: Array,
      required: true,
      default: () => [1]
    },
    oldPrice: {
      type: String,
      default: null
    },
    newPrice: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    isCart: {
      type: Boolean,
      required: true
    }
  },
  data () {
    return {
      currentImageIndex: sessionStorage.getItem('selectedImageIndex') ? parseInt(sessionStorage.getItem('selectedImageIndex')) : 0
    }
  },
  computed: {
    currentImage () {
      return this.images && this.images.length > 0 ? this.images[this.currentImageIndex] : ''
    }
  },
  methods: {
    closeModal () {
      this.$emit('close')
    },
    nextImage () {
      if (this.images && this.images.length > 1) {
        this.currentImageIndex = (this.currentImageIndex + 1) % this.images.length
        sessionStorage.setItem('selectedImageIndex', this.currentImageIndex)
      }
    },
    prevImage () {
      if (this.images && this.images.length > 1) {
        this.currentImageIndex = (this.currentImageIndex - 1 + this.images.length) % this.images.length
        sessionStorage.setItem('selectedImageIndex', this.currentImageIndex)
      }
    }
  },
  setup (props, { emit }) {
    const isInCart = ref(false)
    const isProcessing = ref(false)

    // Загружается состояние из localStorage
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
  }
}
</script>

<style lang="scss">
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;

  .modal-content {
    background-color: white;
    padding: 24px;
    position: relative;
    width: 700px;
    height: 700px;
    max-width: 100%;
    text-align: center;
    display: flex;
    flex-direction: column;

    .close-btn {
      position: absolute;
      top: 10px;
      right: 10px;
      background: none;
      border: none;
      font-size: 20px;
    }

    .slider-content{
      width: 100%;
      display: flex;
      flex-direction: column;
      gap: 16px;
      text-align: left;
      margin: 16px auto 16px;
      flex-grow: 1;
      align-items: flex-start;

      h2{
        font-size: 24px;
        font-weight: 700;
        color: #343030;
      }

      p{
        height: 100%;
        font-size: 14px;
        line-height: 21px;
      }

      .prices{
        display: flex;
        flex-direction: row;
        gap: 12px;

        .old-price {
          text-decoration: line-through;
          font-size: 14px;
          margin-right: 10px;
          color: #A0A0A0;
        }
        .new-price {
          font-size: 18px;
          font-weight: bold;
          color: #343030;
        }
      }

    }
    .slider {
      position: relative;
      width: 652px;
      height: 400px;
      overflow: hidden;
      position: relative;

      .slider-btn {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        background: rgba(0, 0, 0, 0.5);
        color: white;
        border: none;
        font-size: 20px;
        cursor: pointer;

        &.prev-btn {
          left: 10px;
        }
        &.next-btn {
          right: 10px;
        }
      }

      .slider-image {
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }
  }
}
</style>
