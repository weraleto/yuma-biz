<template>
  <div>
    <ProductsHeader
      title="YUMA-POS"
      subtitle="Система автоматизации c бесплатной техподдержкой 24/7 для роста бизнеса"
      button-text="Попробовать"
      :button-subtext="['Попробуйте бесплатно!', '7 дней безлимитного демо-доступа']"
    >
      <picture data-not-lazy>
        <source media="(min-width:1500px)" srcset="~assets/img/header2x.jpg" data-not-lazy>
        <source media="(min-width:700px)" srcset="~assets/img/header.jpg" data-not-lazy>
        <source media="(min-width:0px)" srcset="~assets/img/header0.5.jpg" data-not-lazy>
        <img src="~assets/img/header.jpg" alt="yuma pos" data-not-lazy>
      </picture>
    </ProductsHeader>
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
        <div class="block-offset__content text-blocks plain ladder-xs-enabled">
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
  import { peculiarities, yumaBizFAQ } from '@/assets/dataContent.js'
  import Collapse from '@/components/collapse'
  import ProductsHeader from '@/components/products-header'
  import Hint from '@/components/popover'
  import Peculiarities from '@/components/tabs-swipered'
  import LeadForm from '@/components/contact-form'
  export default {
    name: 'IndexPage',
    components: {
      Collapse,
      LeadForm,
      Hint,
      Peculiarities,
      ProductsHeader
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
        faq: yumaBizFAQ
      }
    },
    methods: {}
  }
</script>

<style lang="scss">
  @import '@/assets/scss/_variables';
  @import '@/assets/scss/components/block-offset';

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