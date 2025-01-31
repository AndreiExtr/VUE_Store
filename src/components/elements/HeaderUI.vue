<template>
  <header class="header">
    <div class="header__content">
      <!-- Бургер-меню / Крестик для закрытия -->
      <button class="burger-menu" @click="toggleMenu">
        <svg class="burger-icon" :class="{ 'active': isMenuOpen }" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="30" height="30">
          <path :d="isMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'" stroke="#333" stroke-width="2" fill="none" />
        </svg>
      </button>
      <nav class="nav" :class="{ 'nav--open': isMenuOpen }">
        <ul class="nav-list">
          <li class="nav-item">Каталог</li>
          <li class="nav-item">Доставка</li>
          <li class="nav-item">Оплата</li>
          <li class="nav-item">Контакты</li>
          <li class="nav-item">О компании</li>
        </ul>
      </nav>

      <!-- Мобильное меню -->
      <MobileMenu :isMenuOpen="isMenuOpen" @close="closeMenu" />

      <SearchUI class="search-bt" @search="handleSearch"/>
    </div>
  </header>
</template>

<script>
import SearchUI from './SearchUI.vue'
import MobileMenu from './MobileMenu.vue'

export default {
  name: 'HeaderUI',
  components: {
    SearchUI,
    MobileMenu
  },
  data () {
    return {
      searchQuery: '',
      isMenuOpen: false
    }
  },
  emits: ['search'],
  methods: {
    handleSearch (query) {
      this.$emit('search', query)
    },
    toggleMenu () {
      this.isMenuOpen = !this.isMenuOpen
    },
    closeMenu () {
      this.isMenuOpen = false
    }
  }
}
</script>

<style lang="scss">
  .header{
    width: 100%;
    height: 97px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    border-bottom: 1px solid #E1E1E1;

    @media (max-width: 992px) {
      position: fixed;
      background-color: #f6f3f3;
      z-index: 3;
    }

    &__content{
      width: 1216px;
      display: flex;
      flex-direction: row;
      justify-content: space-between;

      @media (max-width: 1280px) {
        padding: 0 24px;
      }

      /* Бургер-меню */
      .burger-menu {
        display: none;
        background: none;
        border: none;
        cursor: pointer;
        position: relative;
        z-index: 11;

        @media (max-width: 992px) {
          display: block;
        }
      }

      .burger-icon {
        width: 30px;
        height: 30px;
        transition: transform 0.3s ease;
        display: block;

        &.active {
          transform: rotate(90deg);
        }
      }

      .nav {
        display: inline;
        padding: 43px 0;

        @media (max-width: 992px) {
          display: none;
        }

        .nav-list {
          display: flex;
          flex-direction: row;
          align-items: center;
          gap: 48px;

          @media (max-width: 1200px) {
            gap: 24px;
          }

          .nav-item {
            cursor: pointer;
            font-size: 14px;
            color: #343030;

            &:hover {
              color: #b9b5b4;
            }
          }
        }
      }

      .search-bt{
        width: 416px;
      }
    }
  }
</style>
