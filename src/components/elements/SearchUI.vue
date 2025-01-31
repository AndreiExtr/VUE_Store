<template>
  <div class="search">
    <input
      v-model="searchQuery"
      type="text"
      class="search-input"
      placeholder="Поиск по названию картины"
    />
    <ButtonUI  :label="'Искать'" :show-icon="false"   @click="handleSearch" />
  </div>
</template>

<script>
import ButtonUI from './ButtonUI.vue'

export default {
  name: 'SearchUI',
  components: {
    ButtonUI
  },
  data () {
    return {
      searchQuery: ''
    }
  },
  emits: ['search'],
  methods: {
    handleSearch () {
      this.$emit('search', this.searchQuery.trim())
    }
  }
}
</script>

<style lang="scss">
.search {
  display: flex;
  align-items: center;
  justify-content: flex-end;

  .search-input {
    width: 100%;
    max-width: 300px;
    height: 48px;
    padding: 8px 12px;
    border: 1px solid #E1E1E1;
    font-size: 14px;
    line-height: 20px;
    color: #343030;

    @media (max-width: 992px) {
      width: 300px;
    }

    @media (max-width: 576px) {
      font-size: 12px;
    }

    &::placeholder {
      color: #9F9F9F;
    }

    &:focus {
      outline: none;
      border-color: #B5B5B5;
      color: #343030;
    }
  }
}
</style>
