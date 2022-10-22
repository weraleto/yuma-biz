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
                <systemComponents :data="systemComponentsData" />
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