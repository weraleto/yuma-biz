<template>
  <div>
    <main class="main products">
        <div class="container">
            <!-- Компоненты системы -->
            <section class="section sys-components">
                <div class="products-title">
                    <h1 class="title1">
                        Компоненты системы
                    </h1>
                    <p class="subtitle">
                        Все компоненты синхронизируются между собой в режиме реального времени. Из них легко собрать решение для задач именно вашего бизнеса.
                    </p>
                </div> 
                <div class="sys-components__picture">
                    <img src="~assets/img/products/sys-prod.jpg" alt="Компоненты системы">
                </div>
                <div class="sys-components__container grid-layout">
                    <div v-for="(item, i) in systemComponentsData" :key="i"
                        class="sys-components__item"
                        :class="[`col-${item.colspan}`, `row-${item.rowspan}`]"
                    >
                        <div class="sys-components__item--front">
                            <h4 class="subtitle sys-components__item--front__title">{{item.frontTitle}}</h4>
                            <p>{{item.frontText}}</p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Полный перечень тарифов YUMA-POS -->
            <section class="section tariffs">
                <div class="tariffs__title">
                    <div class="products-title">
                        <h1 class="title1">
                            Полный перечень тарифов YUMA-POS
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
import Tariffs from '../components/tabs-faq'
export default {
    name: 'ProductsPage',
    components: {
        LeadForm,
        calculatorIcon,
        Tariffs
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
    $--products-default-border-radius: 12px;

    .products {
        &-title {
            max-width: 50%;
            margin-bottom: 52px;

            p {
                margin-top: 16px;
            }
        }
    }

    .sys-components {
        &__picture {
            border-radius: $--products-default-border-radius;
            overflow: hidden;
            margin-bottom: 36px;
        }

        &__container {
            gap: 20px;
            grid-auto-flow: column dense;
            grid-template-rows: repeat(3, 240px);
        }
        
        &__item {
            border-radius: $--products-default-border-radius;
            border: 1px solid $--gray-medium;
            padding: 36px;
            position: relative;
            cursor: pointer;

            &::after {
                content: '';
                width: 22px;
                height: 22px;
                position: absolute;
                bottom: 33px;
                right: 33px;
                background: url('../assets/img/arrow.svg') no-repeat center center;
                background-size: cover;
                transition: transform .3s ease;
            }

            &:hover {
                &::after {
                    transform: translate(30%, 30%);
                }
            }

            &.col-1 {
                grid-column: span 3;
            }
            &.col-2 {
                grid-column: span 6;
            }
            &.row-2 {
                grid-row: span 2;
            }
            &--front {
                &__title {
                    margin-bottom: 12px;
                }
            }
        }
    }

    .tariffs {
        &__title {
            display: flex;

            &--icon {
                width: 100%;
                display: flex;
                justify-content: center;
                align-items: center;
            }
        }
    }
</style>