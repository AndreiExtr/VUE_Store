<template>
  <div class="mobile-menu" :class="{ 'mobile-menu--open': isMenuOpen }">
    <!-- Меню -->
    <nav class="navigation">
      <ul class="nav-list">
        <li class="nav-item">Каталог</li>
        <li class="nav-item">Доставка</li>
        <li class="nav-item">Оплата</li>
        <li class="nav-item">Контакты</li>
        <li class="nav-item">О компании</li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  props: {
    isMenuOpen: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    closeMenu () {
      this.$emit('close')
    }
  }
}
</script>

<style scoped lang="scss">
.mobile-menu {
  position: fixed;
  top: 0;
  right: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: none;
  justify-content: center;
  align-items: center;
  transition: transform 0.3s ease;
  z-index: 1;

  &.mobile-menu--open {
    display: flex;
    background-color: #f6f3f3;
    transform: translateX(0);
  }

  .navigation {
    background-color: #f6f3f3;
    width: 100%;
    padding: 20px;

    .nav-list {
      display: flex;
      flex-direction: column;
      gap: 24px;
      align-items: center;
    }

    .nav-item {
      cursor: pointer;
      font-size: 18px;
      color: #343030;

      &:hover {
        color: #b9b5b4;
      }
    }
  }

  .close-menu {
    background: none;
    border: none;
    position: absolute;
    top: 20px;
    right: 20px;
    cursor: pointer;

    svg {
      fill: #333;
    }
  }
}
</style>
