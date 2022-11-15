<template>
  <div>
    <header class="header">
      <div class="container header__container">
        <h1>YUMA-pos</h1>
        <h2>Кастомная система автоматизации c бесплатной техподдержкой 24/7</h2>
        <div class="header__promo">
          <div class="header__promo--text">
            <p class="text4">Попробуйте бесплатно!</p>
            <p class="text4">7 дней безлимитного доступа</p>
          </div>
          <button class="btn primary large text4" 
                  @click.prevent="$store.commit('setShowModal', {key: 'showApplyForm', val: true})"
          >Попробовать</button>
        </div>
      </div>
      <div class="header__top">
        <picture data-not-lazy>
          <source media="(min-width:1500px)" srcset="~assets/img/header2x.jpg" data-not-lazy>
          <source media="(min-width:700px)" srcset="~assets/img/header.jpg" data-not-lazy>
          <source media="(min-width:0px)" srcset="~assets/img/header0.5.jpg" data-not-lazy>
          <img src="~assets/img/header.jpg" alt="yuma pos" data-not-lazy>
        </picture>
      </div>
    </header>
    <main>
      <!-- Система учитывает ваши особенности бизнеса -->
      <section class="block-offset grid-layout">
        <h2 class="title1 container block-offset__title">Система учитывает ваши 
          особенности бизнеса</h2>
          <Peculiarities id="peculiarities" :tabs-content="peculiarities" image-folder-name="peculiarities" />
      </section>

      <!-- Процесс подключения к системе -->
      <section class="block-offset grid-layout container">
        <h2 class="title1 block-offset__title">Процесс подключения
          к системе</h2>
        <div class="block-offset__content text-blocks plain">
          <div class="text-blocks__col">
            <div class="text-blocks__item">
              <div class="text-blocks__item-step">01</div>
              <h3 class="subtitle text-blocks__item-subtitle">Оформляем официальные документы</h3>
              <p class="text6">Мы готовим и согласовываем договор, передаём счёт для оплаты выбранного вами решения и
                начинаем работу.</p>
            </div>
            <div class="text-blocks__item">
              <div class="text-blocks__item-step">02</div>
              <h3 class="subtitle text-blocks__item-subtitle">Подготавливаем компоненты системы</h3>
              <p class="text6">Мы запрашиваем необходимую информацию и запускаем для вас программную платформу YUMA-POS.
                <br>А также организуем подключение техники и сервисов.</p>
            </div>
          </div>
          <div class="text-blocks__col">
            <div class="text-blocks__item">
              <div class="text-blocks__item-step">03</div>
              <h3 class="subtitle text-blocks__item-subtitle">Помогаем с переносом данных, если это вам требуется
                <Hint
                  content="Мы расскажем, как перенести данные самостоятельно. А если захотите, то сделаем это за вас. Цены вы можете посмотреть на странице «Компоненты и тарифы»">
                </Hint>
              </h3>
              <p class="text6">Мы готовы помочь вам перейти с прошлой системы и перенести меню с модификаторами, а также
                базу ваших гостей.</p>
            </div>
            <div class="text-blocks__item">
              <div class="text-blocks__item-step">04</div>
              <h3 class="subtitle text-blocks__item-subtitle">Проводим бесплатное обучение</h3>
              <p class="text6">Мы обучаем вас работе в системе и продвижению с помощью маркетинговых инструментов,
                встроенных в YUMA-POS. Ваш бизнес готов выходить на новый уровень эффективности!</p>
            </div>
          </div>
        </div>
      </section>

      <!-- С нами уже работают -->
      <section class="block-offset grid-layout">
        <h2 class="title1 container block-offset__title">С нами уже работают</h2>
        <Partners />
      </section>
      
      <!-- FAQ -->
      <section class="faq-section container">
        <h3 class="title1">Ответы на вопросы бизнеса</h3>
        <div class="faq-section__content">
          <Collapse :data="faq" />
        </div>
      </section>

      <!-- Форма -->
      <LeadForm theme="light" title="Наши специалисты помогут подобрать оптимальное решение ваших задач"
        subtitle="Заполните форму, и мы вас проконсультируем" />
    </main>


  </div>
</template>

<script>
  import { peculiarities, mainPageFAQ } from '@/assets/dataContent.js'
  import Collapse from '../components/collapse'
  import Partners from '../components/partners'
  import Hint from '../components/popover'
  import Peculiarities from '../components/tabs-swipered'
  import LeadForm from '../components/contact-form'
  export default {
    name: 'IndexPage',
    components: {
      Collapse,
      LeadForm,
      Partners,
      Hint,
      Peculiarities
    },
    head() {
      return {
        meta: [
          {
            property: 'og:site_name',
            content: '',
            vmid: 'og:site_name',
            hid: 'og:site_name'
          },
          {
            property: 'og:locale',
            content: 'ru_RU',
            vmid: 'og:locale',
            hid: 'og:locale'
          },
          {
            property: 'og:locale:alternate',
            content: 'en_US',
            vmid: 'og:locale:alternate',
            hid: 'og:locale:alternate'
          },
        ]
      }
    },
    data: () => {
      return {
        peculiarities: peculiarities,
        faq: mainPageFAQ
      }
    },
    methods: {}
  }
</script>

<style lang="scss">
  @import '@/assets/scss/_variables.scss';

  .header {
    margin-bottom: 50px;
    h1 {
      font-size: 134px;
      text-transform: uppercase;
      font-weight: 800;
      margin-bottom: 24px;

      @media screen and (max-width: $--screen-lg-min) {
        font-size: 15vw;
      }
      @media screen and (max-width: $--screen-xs-min) {
        margin-bottom: 12px;
      }
    }

    h2 {
      font-weight: 500;
      font-size: 61px;
      text-transform: uppercase;
      @media screen and (max-width: $--screen-lg-min) {
        font-size: 7.47vw;
        line-height: 1.42em;
      }
    }

    &__top {
      max-height: 70vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: flex-end;
      position: relative;
      picture, img {
        height: 700px;
        width: 100%;
        object-fit: cover;

        @media screen and (max-width: 700px)  {
          height: auto;
          width: 100%;
        }
      }
      
    }

    &__container {
      padding-top: 110px;
      padding-bottom: 150px;
      @media screen and (max-width: $--screen-sm-min) {
        padding-bottom: 72px;
      }
      @media screen and (max-width: $--screen-xs-min) {
        padding-top: 32px;
      }
    }

    &__promo {
      max-width: 264px;
      margin: 60px auto 0;
      text-align: center;

      &--text {
        margin-bottom: 28px;
      }
    }

    @media screen and (max-width: $--screen-xs-min) {
      margin-bottom: 32px;
    }
  }

  .faq-section {
    padding-bottom: 150px;
    &__content {
      margin-top: 52px;
      @media screen and (max-width: $--screen-sm-min) {
        margin-top: 24px;
      }
    }
  }
</style>