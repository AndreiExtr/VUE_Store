<template>
  <div class="home">
    <HeaderUI @search="handleSearch"/>
    <main class="home__content">
      <h1>Картины эпохи Возрождения</h1>
      <div class="cards">
        <CardUI
          v-for="(painting, index) in filteredPaintings"
          :key="index"
          :image="painting.image"
          :title="painting.title"
          :oldPrice="painting.oldPrice"
          :newPrice="painting.newPrice"
          :description="painting.description"
          :showText="painting.isSold"
          :showPrice="painting.isPrSold"
          @click="openModal(painting)"
          @update-cart="updateModalState"
        />
      </div>
    </main>
    <FooterUI />
    <ModalView
      v-if="isModalVisible"
        :isVisible="isModalVisible"
        :title="selectedPainting.title"
        :images="selectedPainting.images"
        :oldPrice="selectedPainting.oldPrice"
        :newPrice="selectedPainting.newPrice"
        :description="selectedPainting.description"
        :isInCart="isInCart"
        @close="closeModal"
    />
  </div>
</template>

<script>
import CardUI from '@/components/elements/CardUI.vue'
import HeaderUI from '@/components/elements/HeaderUI.vue'
import FooterUI from '@/components/elements/FooterUI.vue'
import ModalView from './ModalView.vue'
import { ref } from 'vue'

export default {
  name: 'HomeView',
  components: {
    CardUI,
    HeaderUI,
    FooterUI,
    ModalView
  },
  data () {
    return {
      searchQuery: sessionStorage.getItem('searchQuery') || '',
      isModalVisible: sessionStorage.getItem('isModalVisible') === 'true',
      selectedPainting: JSON.parse(sessionStorage.getItem('selectedPainting')) || {},
      paintings: [
        { image: '1.png', isSold: false, isPrSold: true, title: '«Рождение Венеры» Сандро Боттичелли', oldPrice: '2 000 000', newPrice: '1 000 000', images: [require('@/assets/1.png'), require('@/assets/1_1.jpg'), require('@/assets/1_2.jpg')], description: '«Рождение Венеры» — это картина итальянского художника Сандро Боттичелли, которую он завершил приблизительно к 1485 году.' },
        { image: '2.png', isSold: false, isPrSold: true, title: '«Тайная вечеря» Леонардо да Винчи', oldPrice: null, newPrice: '3 000 000', images: [require('@/assets/2.png'), require('@/assets/2_1.jpg'), require('@/assets/2_2.jpg')], description: '«Тайная вечеря» — монументальная роспись Леонардо да Винчи, изображающая последнюю трапезу Христа с учениками.' },
        { image: '3.png', isSold: false, isPrSold: true, title: '«Сотворение Адама» Микеланджело', oldPrice: '6 000 000', newPrice: '5 800 000', images: [require('@/assets/3.png'), require('@/assets/3_1.jpg'), require('@/assets/3_2.jpg')], description: '«Сотворение Адама» — фреска Микеланджело, написанная около 1511 года. Является четвёртой из девяти центральных композиций потолка Сикстинской капеллы, посвящённых девяти сюжетам книги Бытия.' },
        { image: '4.png', isSold: true, isPrSold: false, title: '«Урок анатомии»  Рембрандт', oldPrice: '10 000 000', newPrice: '8 000 000', images: [require('@/assets/4.png'), require('@/assets/4_1.jpg'), require('@/assets/4_2.jpg')], description: '«Урок анатомии доктора Тульпа» — картина выдающегося голландского живописца Рембрандта ван Рейна, написанная в 1632 году.' }
      ]
    }
  },
  computed: {
    filteredPaintings () {
      if (!this.searchQuery) return this.paintings
      return this.paintings.filter(painting =>
        painting.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      )
    }
  },
  methods: {
    handleSearch (query) {
      this.searchQuery = query
      sessionStorage.setItem('searchQuery', query)
    },
    openModal (painting) {
      this.selectedPainting = painting
      this.isModalVisible = true
      sessionStorage.setItem('isModalVisible', 'true')
      sessionStorage.setItem('selectedPainting', JSON.stringify(painting))
    },
    closeModal () {
      this.isModalVisible = false
      this.selectedPainting = {}
      sessionStorage.setItem('isModalVisible', 'false')
      sessionStorage.setItem('selectedImageIndex', 0)
    }
  },
  setup () {
    const isModalOpen = ref(false)
    const selectedProduct = ref({})

    const updateModalState = (title, state) => {
      if (selectedProduct.value.title === title) {
        selectedProduct.value.isInCart = state
      }
    }

    return {
      isModalOpen,
      selectedProduct,
      updateModalState
    }
  }
}
</script>

<style lang="scss">
.home{
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;

  &__content{
    width: 100%;
    max-width: 1216px;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;

    h1{
      color: #343030;
      font-size: 24px;
      font-weight: 700;
      text-align: left;
      margin-bottom: 39px;
      margin-top: 45px;
    }

    .cards{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
    }
  }
}
</style>
