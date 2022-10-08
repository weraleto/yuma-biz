<template>
  <div>
    <header class="header">
      <div class="header__top">
        <picture>
          <source media="(min-width:1900px)" srcset="~assets/img/header@2x.jpg">
          <source media="(min-width:990px)" srcset="~assets/img/header.jpg">
          <source media="(min-width:230px)" srcset="~assets/img/header@0.5.jpg">
          <img src="~assets/img/header.jpg" alt="yuma pos">
        </picture>
      </div>
      <div class="container header__container">
        <h1>YUMA-pos</h1>
        <h2>Кастомная система автоматизации c бесплатной техподдержкой 24/7</h2>
        <div class="header__promo">
          <div class="header__promo--text">
            <p class="text4">Попробуйте бесплатно!</p>
            <p class="text4">7 дней безлимитного доступа</p>
          </div>
          <button class="btn primary large subtitle" @click.prevent>Попробовать</button>
        </div>
      </div>
    </header>
    <main>
      <!-- Система учитывает ваши особенности бизнеса -->
      <section class="block-offset grid-layout">
        <h2 class="title1 container block-offset__title">Система учитывает ваши 
          особенности бизнеса</h2>
          <Peculiarities id="peculiarities" image-folder-name="peculiarities" />
      </section>

      <!-- Поцесс подключения к системе -->
      <section class="block-offset grid-layout container">
        <h2 class="title1 block-offset__title">Поцесс подключения
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

      <!-- Форма -->
      <LeadForm theme="light" title="Наши специалисты помогут подобрать оптимальное решение ваших задач"
        subtitle="Заполните форму, и мы вас проконсультируем" />
      
      <!-- FAQ -->
      <section class="pt-large faq-section">
        <div class="container--large">
          <h3 class="title1">Ответы на вопросы бизнеса</h3>
        </div>
        <div class="container faq-section__content">
          <Collapse :data="faq" />
        </div>
      </section>
    </main>


  </div>
</template>

<script>
  import Collapse from '../components/collapse'
  import Partners from '../components/partners'
  import Hint from '../components/popover'
  import Peculiarities from '../components/tabs'
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
        title: 'HelloWorld',
        meta: [{
            hid: 'description',
            name: 'description',
            content: ''
          },
          {
            property: 'og:title',
            content: '',
            vmid: 'og:title',
            hid: 'og:title'
          },
          {
            property: 'og:description',
            content: '',
            vmid: 'og:description',
            hid: 'og:description'
          },
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
        faq: [{
            title: 'Как решает вопросы техподдержка?',
            text: 'Наши специалисты ведут живое общение по телефону. А также вы всегда можете обратиться к ним в популярных мессенджерах.'
          },
          {
            title: 'Как быстро получится начать работу в системе?',
            text: 'Мы готовы подключить вам фронт кассира и бэк-офис в течение 1 рабочего дня. И ваши заведения уже смогут начать работу в системе.</br></br>Сроки по остальным компонентам мы согласуем с вами дополнительно. Они будут зависеть, в том числе, от скорости предоставления вами необходимых материалов (иллюстраций, описаний ваших блюд и акций, т.д.)'
          },
          {
            title: 'Требуются ли для работы с YUMA-POS собственные серверы, а также технические специалисты или сисадмины?',
            text: 'Никакой специальной техники и специалистов от вас не требуется. YUMA-POS - полностью облачное решение, работающее на российских серверах крупнейшей отечественной платформы Яндекс.Облако. Техподдержку вашей системы и приложений мы полностью берем на себя. '
          },
          {
            title: 'Если у меня уже есть свой сайт или мобильное приложение, могу я подключить их к системе YUMA-POS?',
            text: 'Сторонние мобильное приложение и сайт могут работать только без интеграции с нашей системой.</br></br>Как правило, бизнесу удобнее наше комплексное решение.  Мы запускаем наше мобильное приложение и сайт как часть системы автоматизации. Это просто, быстро и обеспечивает ресторанному предприятию полную синхронизацию учета и каналов продаж. '
          },
          {
            title: 'Можно ли приобрести у вас только мобильное приложение и сайт?',
            text: 'Это, к сожалению, невозможно, т.к. мобильное приложение и сайт являются частью системы автоматизации YUMA-POS и запускаются только на ее платформе.'
          },
          {
            title: 'Как происходят обновления системы?',
            text: 'Мы уже давно работаем в ресторанной сфере, ориентируемся в потребностях бизнеса и постоянно развиваем YUMA-POS в соответствии с ними. Все компоненты на устройствах наших пользователей обновляются дистанционно и полностью бесплатно.'
          }
        ]
      }
    },
    methods: {}
  }
</script>

<style lang="scss">
  @import '@/assets/scss/_variables.scss';

  .header {
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
      }
    }

    &__top {
      height: 700px;
      max-height: 70vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: flex-end;
      picture, source, img {
        height: auto;
        width: 100%;
      }
      @media screen and (max-width: $--screen-lg-min) {
        height: 637px;
        max-height: 65vh;
        picture, source, img {
          height: 100%;
          width: auto;
        }
      }
    }

    &__container {
      padding-top: 60px;
      padding-bottom: 100px;
      @media screen and (max-width: $--screen-xs-min) {
        padding-top: 32px;
        padding-bottom: 72px;
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
  }

  .faq-section {
    &__content {
      margin-top: 52px;
      @media screen and (max-width: $--screen-sm-min) {
        margin-top: 24px;
      }
    }
  }
</style>