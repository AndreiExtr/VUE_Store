<template>
  <footer class="footer">
    <div class="footer__content">
      <nav class="nav">
        <ul class="nav-list">
          <li class="nav-item">Каталог</li>
          <li class="nav-item">Доставка</li>
          <li class="nav-item">Оплата</li>
          <li class="nav-item">Контакты</li>
          <li class="nav-item">О компании</li>
        </ul>
      </nav>

      <div class="contacts">
        <div class="number">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M14.6861 12.0733L12.5241 9.9061C12.0934 9.47621 11.3803 9.48927 10.9346 9.9361L9.84534 11.0276C9.77652 10.9896 9.70529 10.9499 9.6304 10.9077C8.94254 10.5257 8.00109 10.0022 7.0104 9.00851C6.01678 8.01276 5.49391 7.06772 5.11161 6.37786C5.07127 6.30478 5.03261 6.23431 4.99445 6.16739L5.7255 5.43577L6.08492 5.07509C6.53125 4.62763 6.54356 3.91305 6.11392 3.48192L3.95184 1.31445C3.52219 0.883917 2.80871 0.896979 2.36238 1.34444L1.75303 1.95868L1.76968 1.97525C1.56536 2.23655 1.39462 2.53793 1.26756 2.86292C1.15044 3.17228 1.07752 3.46748 1.04418 3.76329C0.758688 6.13542 1.84023 8.30337 4.7754 11.2452C8.8327 15.3114 12.1023 15.0043 12.2434 14.9893C12.5506 14.9525 12.845 14.8789 13.1442 14.7624C13.4657 14.6366 13.7662 14.4657 14.0267 14.2613L14.04 14.2732L14.6573 13.6673C15.1028 13.22 15.1156 12.5051 14.6861 12.0733Z" fill="#555555"/>
          </svg>
          <p>+7 (812) 555-55-55</p>
        </div>

        <div class="adress">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M8.07028 1C5.27451 1 3 3.27451 3 6.07025C3 9.53985 7.5374 14.6334 7.73058 14.8486C7.91204 15.0507 8.22884 15.0503 8.40997 14.8486C8.60315 14.6334 13.1406 9.53985 13.1406 6.07025C13.1405 3.27451 10.866 1 8.07028 1ZM8.07028 8.62123C6.66366 8.62123 5.51932 7.47687 5.51932 6.07025C5.51932 4.66363 6.66368 3.51929 8.07028 3.51929C9.47687 3.51929 10.6212 4.66366 10.6212 6.07028C10.6212 7.47689 9.47687 8.62123 8.07028 8.62123Z" fill="#555555"/>
          </svg>
          <p>г. Санкт-Петербург, ул. Ефимова, 3</p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'FooterUI',
  components: {
  },
  props: {}
}
</script>

<style lang="scss">
  .footer{
    width: 100%;
    height: 97px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    background-color: #ECEAEA;
    align-items: center;

    &__content{
      width: 1216px;
      display: flex;
      flex-direction: row;
      justify-content: space-between;

      @media (max-width: 1280px) {
        padding: 0 24px;
      }

      @media (max-width: 576px) {
        display: flex;
        flex-direction: column;
        justify-content: left;
        padding: 0 16px;
      }

      .nav {
        display: flex;
        padding: 0;

        .nav-list {
          display: flex;
          flex-direction: row;
          align-items: center;
          gap: 48px;

          .nav-item {
            display: inline;
            cursor: pointer;
            font-size: 14px;
            color: #555555;

            &:hover {
              color: #b9b5b4;
            }

            @media (max-width: 1280px) {
              display: none;
            }
          }
        }
      }

      .contacts{
        display: flex;
        flex-direction: row;
        gap: 51px;
        font-size: 14px;
        color: #555555;

        @media (max-width: 576px) {
          display: flex;
          flex-direction: column;
          gap: 24px;
        }

        .number,
        .adress{
          display: flex;
          flex-direction: row;
          align-items: center;
          gap: 8px;
        }
      }
    }
  }
</style>
