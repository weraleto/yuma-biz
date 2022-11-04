<template>
  <div>
    <main class="main products">
        <div class="container">
            <!-- Компоненты системы -->
            <section class="section sys-components">
                <div class="section-title sys-components__title">
                    <h1 class="title1">
                        Компоненты системы
                    </h1>
                    <p class="section-subtitle subtitle">
                        Все компоненты синхронизируются между собой в режиме реального времени. Из них легко собрать решение для задач именно вашего бизнеса.
                    </p>
                </div> 
                 <div class="sys-components__picture">
                    <picture data-not-lazy>
                        <source media="(min-width:1500px)" srcset="~assets/img/products/sys-prod.jpg" data-not-lazy>
                        <source media="(min-width:700px)" srcset="~assets/img/products/sys-prod@0.75x.jpg" data-not-lazy>
                        <source media="(min-width:0px)" srcset="~assets/img/products/sys-prod@0.5x.jpg" data-not-lazy>
                        <img src="~assets/img/products/sys-prod.jpg" alt="Компоненты системы" data-not-lazy>
                    </picture>
                    <!-- <img v-lazy-load data-src="~assets/img/products/sys-prod.jpg" alt="Компоненты системы"> -->
                </div> 
                <systemComponents :data="systemComponentsData" />
            </section>

            <!-- Полный перечень тарифов YUMA-POS -->
            <section class="section tariffs">
                <div class="tariffs__title">
                    <div class="products-title">
                        <h1 class="title1">
                            Полный перечень тарифов <span class="no-word-break">YUMA-POS</span>
                        </h1>
                        <p class="subtitle">
                            Весь необходимый для запуска сервис мы предоставляем бесплатно. Если вам понадобится что-то большее, то можно заказать дополнительные услуги.
                        </p>
                    </div>
                    <div class="tariffs__title--icon">
                        <calculatorIcon />
                    </div>
                </div>
                <div class="tariffs__container grid-layout">
                    <Tariffs id="tariffs" :data="tariffs" />
                </div>
            </section>
        </div>

        <!-- Форма -->
      <LeadForm theme="light" title="Наши специалисты помогут подобрать оптимальное решение ваших задач"
        subtitle="Заполните форму, и мы вас проконсультируем" />
    </main>
  </div>
</template>

<script>
import { tariffs, systemComponentsData } from '@/assets/dataContent.js'
import calculatorIcon from '../components/svg/сalculator'
import LeadForm from '../components/contact-form'
import systemComponents from '../components/system-components'
import Tariffs from '../components/tabs-faq'
export default {
    name: 'ProductsPage',
    components: {
        LeadForm,
        calculatorIcon,
        Tariffs,
        systemComponents
    }, 
    data: () => {
        return {
            systemComponentsData: systemComponentsData,
            tariffs: tariffs
        }
    }
}
</script>

<style lang="scss">
    @import '@/assets/scss/_variables';

    .sys-components {
        &__title {
            margin-bottom: 52px;
        }
        &__picture {        
            margin-bottom: 36px;

            @media screen and (min-width: calc($--screen-xs-min + 1px)) {
                border-radius: $--products-default-border-radius;
                overflow: hidden;
            }

            @media screen and (max-width: $--screen-sm-min) {
                picture, img {
                    width: 100vw;
                    height: 220px;
                    object-fit: cover;
                }
            }
            @media screen and (max-width: $--screen-xs-min) {
                margin-bottom: 24px;
                picture, img {
                    transform: translateX(-16px);
                    height: 51.73vw;
                }
            }
        }
    }

    .tariffs {
        &__title {
            display: flex;
            margin-bottom: 68px;

            &--icon {
                width: 100%;
                display: flex;
                justify-content: center;
                align-items: center;
            }

            @media screen and (max-width: $--screen-sm-min) {
                flex-direction: column; 
                gap: 16px;
                margin-bottom: 54px;

                &--icon {
                    align-items: flex-start;
                }   
            }
        }
    }
</style>