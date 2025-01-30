<template>
  <header class="header">
    <div class="header__content">
      <nav class="nav">
        <ul class="nav-list">
          <li class="nav-item">Каталог</li>
          <li class="nav-item">Доставка</li>
          <li class="nav-item">Оплата</li>
          <li class="nav-item">Контакты</li>
          <li class="nav-item">О компании</li>
        </ul>
      </nav>
      <SearchUI class="search-bt" @search="handleSearch"/>
    </div>
  </header>
</template>

<script>
import SearchUI from './SearchUI.vue'

export default {
  name: 'HeaderUI',
  components: {
    SearchUI
  },
  data () {
    return {
      searchQuery: ''
    }
  },
  emits: ['search'],
  methods: {
    handleSearch (query) {
      this.$emit('search', query)
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

    &__content{
      width: 1216px;
      display: flex;
      flex-direction: row;
      justify-content: space-between;

      .nav {
        display: flex;
        padding: 43px 0;

        .nav-list {
          display: flex;
          flex-direction: row;
          align-items: center;
          gap: 48px;

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
