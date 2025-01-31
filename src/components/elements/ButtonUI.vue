<template>
  <button class="custom-button" :disabled="isProcessing" :class="buttonClass" >
    <span v-if="isProcessing" class="loader"></span>
    <span v-if="showIcon" class="button-icon">
      <!-- Иконка лупы для мобильных устройств -->
      <!-- <svg v-if="isMobile" width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M23 21l-6-6M10 16a6 6 0 1 0 0-12 6 6 0 0 0 0 12z" stroke="#333" stroke-width="2" fill="none"/>
      </svg> -->
      <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <g clip-path="url(#clip0_20233_57)">
          <path
            d="M16.5315 4.80937L7.63341 14.237L3.34814 10.1924"
            stroke="#F4F6F9"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </g>
        <defs>
          <clipPath id="clip0_20233_57">
            <rect width="20" height="20" fill="white" />
          </clipPath>
        </defs>
      </svg>
    </span>
    <span class="button-text" v-if="!isProcessing">{{ label }}</span>
  </button>
</template>

<script>
import { computed } from 'vue'
export default {
  name: 'ButtonUI',
  props: {
    showIcon: {
      type: Boolean,
      default: true
    },
    label: {
      type: String,
      default: 'Купить'
    },
    isInCart: {
      type: Boolean,
      default: false
    },
    isProcessing: {
      type: Boolean,
      default: false
    }
  },
  setup (props) {
    const buttonClass = computed(() => {
      return [
        'custom-button',
        props.isProcessing ? 'disabled' : '',
        props.isInCart ? 'in-cart' : ''
      ]
    })

    return {
      buttonClass
    }
  }
}
</script>

<style lang="scss">
.in-cart {
  background-color: #5B3A32 !important; /* После клика "В корзину" */
  color: #F4F6F9 !important;
}
.custom-button {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  width: 118px;
  height: 48px;
  background-color: #382E2B;
  color: #F4F6F9;
  border: none;
  font-size: 14px;
  font-weight: 700;
  line-height: 21px;
  cursor: pointer;
  transition: background-color 0.1s;

  &:hover {
    background-color: #776763;
  }

  &.disabled {
    background-color: #C1B4B1;
    cursor: not-allowed;
    pointer-events: none;
  }

  .button-icon {
    display: flex;
    align-items: center;
  }

  .button-text {
    display: flex;
    align-items: center;
  }

  .loader {
    border: 4px solid #C1B4B1;
    border-top: 4px solid #382E2B;
    border-radius: 50%;
    width: 24px;
    height: 24px;
    animation: spin 1s linear infinite;

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
  }
}
</style>
