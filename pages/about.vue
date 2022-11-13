<template>
      <main class="main about">
        
            <section class="section stages">
                <div class="container">
                    <div class="section-title about-title">
                        <h1 class="title1">
                            YUMA. Этапы развития.
                        </h1>
                        <p class="section-subtitle subtitle">
                            YUMA - это экосистема автоматизации ресторанного бизнеса. Мы построили её, опираясь на наш опыт и ваши потребности. С её помощью каждое заведение или целая сеть получит полный набор решений для развития и роста.
                        </p>
                    </div>
                </div>
                <div class="stages__wrapper">
                    <div class="stages__container grid-layout">
                        <div class="stages__item">
                            <div class="stages__item--year title1">
                                <div class="inner">
                                    <span>2003</span>
                                </div>
                            </div>
                            <div class="inner stages__item--inner">
                                <h3 class="subtitle text-bold">Начало проектной работы</h3>
                                <p class="text6">Запуск отдельных проектов автоматизации бизнес-процессов для сферы торговли и услуг на международном рынке.</p>
                            </div>
                        </div>
                    </div>
                    <div class="stages__container grid-layout">
                        <div class="stages__item">
                            <div class="stages__item--year title1">
                                <span>2009</span>
                            </div>
                            <div class="inner stages__item--inner">
                                <h3 class="subtitle text-bold">Определение ниши</h3>
                                <p class="text6">Концентрация на задачах ресторанного бизнеса и смежной торговли.</p>
                            </div>
                        </div>
                    </div>
                    <div class="stages__container grid-layout">
                        <div class="stages__item">
                            <div class="stages__item--year title1">
                                <div class="inner">
                                    <span>2015</span>
                                </div>
                            </div>
                            <div class="inner stages__item--inner">
                                <h3 class="subtitle text-bold">Разработка комплексной системы YUMA</h3>
                                <p class="text6">Начало работы с отдельными российскими предприятиями, готовыми к внедрению инноваций.</p>
                            </div>
                        </div>
                    </div>
                    <div class="stages__container grid-layout">
                        <div class="stages__item">
                            <div class="stages__item--year title1">
                                <span>2018</span>
                            </div>
                            <div class="inner stages__item--inner">
                                <h3 class="subtitle text-bold">Фокус развития на российском рынке</h3>
                                <p class="text6">Начат поэтапный выход YUMA на широкий российский рынок.</p>
                            </div>
                        </div>
                    </div>
                    <div class="stages__container grid-layout">
                        <div class="stages__item">
                            <div class="stages__item--year title1">
                                <div class="inner">
                                    <span>2022</span>
                                </div>
                            </div>
                            <div class="inner stages__item--inner">
                                <h3 class="subtitle text-bold">Запуск направления бескассовой торговли</h3>
                                <p class="text6">Выпущен новый продукт — микромаркеты YUMA-SMART</p>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
        <div class="container">
            <section class="section reliability">
                <div class="section-title about-title">
                    <h2 class="title1">
                        Надёжность<br>
                        технологии YUMA
                    </h2>
                </div>
                <div class="grid-layout">
                        <div class="flip-card__items card-items">
                        <div v-for="(item, idx) in reliability" :key="idx" class="card flip-card card-item" 
                            :style="`top: ${ -(41 * idx) }px`"
                        >
                            <div class="flip-card-inner card-item__inner">
                                <div class="flip-card-front card-item__front">
                                    <small class="text5">{{item.small}}</small>
                                    <h4 class="title1">{{item.num}}</h4>
                                </div>
                                <div class="flip-card-back card-item__back">
                                    <p class="text5">{{item.back}}</p>
                                </div>
                            </div>
                        </div>
            </div>
                </div>
            </section>
            <section class="section sertification">
                <div class="section-title about-title">
                    <h2 class="title1">
                        сертификация
                    </h2>
                </div>
                <div class="sertification__container grid-layout">
                    <div class="card sertification__card" @click="sertIdx=0">
                        <p class="title1">
                            ISO 9001
                        </p>
                    </div>
                    <div class="card sertification__card" @click="sertIdx=1">
                        <p class="title1">
                            ISO 27001
                        </p>
                    </div>
                </div>
                <client-only>
                    <div @click="handleGalleryClick">
                        <LightGallery
                            :images="['/sert/iso-9001.png', '/sert/iso-27001.png']"
                            :index="sertIdx"
                            :disable-scroll="true"
                            background="rgba(42, 42, 42, 0.9)"
                            @close="sertIdx = null"
                            ref="sertGallery"
                            />
                    </div>
                </client-only>
            </section>
        </div>
      </main>
</template>

<script>
export default {
    head() {
        return {
            title: 'Экосистема автоматизации ресторанного и торгового бизнеса YUMA',
            meta: [{
                    hid: 'description',
                    name: 'description',
                    content: 'Индивидуальные решения для запуска и развития бизнеса, роста доходов и продвижения вашего заведения или целой сети. Российский разработчик с успешным международным опытом. Сервисная поддержка и маркетинговая платформа в комплекте любого решения.'
                },
                {
                    property: 'og:title',
                    content: 'Экосистема автоматизации ресторанного и торгового бизнеса YUMA',
                    vmid: 'og:title',
                    hid: 'og:title'
                },
                {
                    hid: 'og:description',
                    property: 'og:description',
                    vmid: 'og:description',
                    content: 'Индивидуальные решения для запуска и развития бизнеса, роста доходов и продвижения вашего заведения или целой сети. Российский разработчик с успешным международным опытом. Сервисная поддержка и маркетинговая платформа в комплекте любого решения.'
                },
            ]
        }
    },
    data: () => {
        return {
            reliability: [{
                'num': '1 миллион',
                'small': 'Скачиваний мобильных приложений наших клиентов',
                'back': 'Мы запускаем мобильные приложения, которыми покупатели действительно активно пользуются.'
                },
                {
                'num': '150 тысяч',
                'small': 'Операций покупок у наших клиентов каждый день',
                'back': 'Мы работаем на платформе Яндекс.Облако, способной стабильно и без перебоев поддерживать постоянно высокую нагрузку.'
                },
                {
                'num': '3 ТЫСЯЧИ',
                'small': 'Автоматизированных заведений по всей России',
                'back': 'На платформе YUMA успешно работают предприятия сферы общественного питания всех типов, форматов и масштабов.'
                },
                {
                'num': 'более 12',
                'small': 'Стран мира, где работает технология YUMA',
                'back': 'Великобритания, Ирландия, США, Австралия, Швейцария, Нидерланды, Индия, ОАЭ, ЮАР, Украина, Казахстан, Беларусь, Россия.'
                },
            ],
            sertIdx: null
        }
    },
    methods: {
        handleGalleryClick(e) {
            if (e.target.tagName.toLowerCase() != 'img') {
                this.$refs.sertGallery.close()
            }
        }
    }
}
</script>

<style lang="scss">
    @import '@/assets/scss/_variables.scss';
    @import '@/assets/scss/_mixins.scss';

    .about {
        &-title {
            margin-bottom: 100px;
            @media screen and (max-width: $--screen-md-min) {
                margin-bottom: 50px;
            }
        }
    }

    .stages {
        &__container {
            gap: 0 40px;
            // justify-items: center;
            display: grid;

            &:nth-child(2n-1) {
                
                .stages__item {
                    grid-column: 1/8;
                    align-items: flex-end;
                }
                .stages__item--year {
                    justify-content: flex-end;

                    &::after {
                        width: calc(100% - 290px);
                    }
                    span::after {
                        width: 100%;
                    }
                }
            }
            &:nth-child(2n) {
                .stages__item {
                    grid-column: 9/13;
                }
                .stages__item--year {

                    &::after {
                        width: 100%;
                    }
                }
            }
            @media screen and (max-width: $--screen-sm-min) {
                margin-bottom: 32px;
                padding-left: 16px;
                padding-right: 16px;
                &:nth-child(2n-1) {
                    .stages__item {
                        grid-column: 1/4;
                    }
                    .stages__item--year {
                        &::after {
                            width: 100%;
                            transform: translateX(-90%);
                        }
                    }
                }
                &:nth-child(2n) {
                    .stages__item {
                        grid-column: 3/6;
                    }
                    .stages__item--year {
                        &::after {
                            width: calc(100% + 16px);
                        }
                    }
                }
            }
            @media screen and (max-width: $--screen-xs-min) {
                &:nth-child(2n-1) {
                    .stages__item {
                        grid-column: 1/5;
                    }
                }
                &:nth-child(2n) {
                    .stages__item {
                        grid-column: 2/6;
                    }
                }
            }
        }
        &__item {
            display: flex;
            flex-direction: column;
            width: 100%;

            &--year {
                position: relative;
                width: 100%;
                display: flex;
                margin-bottom: 12px;

                span {
                    display: inline-block;
                    position: relative;
                }
                span::after, &::after {
                    content: '';
                    position: absolute;
                    left: 0;
                    bottom: 0;
                    height: 1px;
                    background-color: $--gray-medium;
                }
            }
            &--inner {
                display: flex;
                flex-direction: column;
                gap: 20px;
            }

            .inner {
                max-width: 290px;
                width: 100%;
                @media screen and (max-width: $--screen-sm-min) {
                    max-width: unset;
                }
            }

            @media screen and (max-width: $--screen-xs-min) {
                .subtitle {
                    font-size: 16px;
                }
            }
        }
    }

    .reliability {
        @media screen and (min-width: calc($--screen-xs-min + 1px)) {
            padding-bottom: 0;
        }
    }

    .sertification {
        &__container {
            gap: 40px;

            @media screen and (max-width: $--screen-sm-min) {
                gap: 10px;
                grid-template-columns: repeat(6, 1fr);
            }

        }
        &__card {
            min-height: 418px;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 10px;
            position: relative;
            cursor: pointer;

            &:nth-child(2n-1) {
                grid-column: 4/7;
            }
            &:nth-child(2n) {
                grid-column: 7/10;
            }
            &::after {
                content: '';
                width: 22px;
                height: 22px;
                position: absolute;
                bottom: 25px;
                right: 25px;
                background: url('../assets/img/arrow.svg') no-repeat center center;
                background-size: cover;
                transition: transform .3s ease;
                z-index: 1;
            }

            &:hover {
                &::after {
                    transform: translate(30%, 30%);
                }
            }

            @media screen and (max-width: $--screen-md-min) {
                min-height: 40.8vw;
                &:nth-child(2n-1) {
                    grid-column: 3/7;
                }
                &:nth-child(2n) {
                    grid-column: 7/11;
                }
            }

            @media screen and (max-width: $--screen-sm-min) {
                &:nth-child(2n-1) {
                    grid-column: 1/4;
                }
                &:nth-child(2n) {
                    grid-column: 4/7;
                }
            }
            @media screen and (max-width: $--screen-xs-min) {
                &:nth-child(2n-1), &:nth-child(2n) {
                    grid-column: 1/7;
                }
            }
        }
    }

    .flip-card__items {
        display: grid;
        grid-auto-flow: column;
        grid-column: 3/12;
        grid-template-columns: repeat(9, 1fr);

        @media screen and (max-width: $--screen-md-min) {
            grid-column: 2/13;
        }
        @media screen and (max-width: $--screen-xs-min) {
            grid-column: 1/6;
        }
    }

    .card-item {
        height: 300px;
        background-color: transparent;
        border-radius: 20px;
        width: 100%;
        position: relative;
        transition: all .3s ease;

        cursor: pointer;

        @media screen and (max-width: $--screen-md-min) {
            height: 25vw;
        }

        @media screen and (max-width: $--screen-sm-min) {
            height: 35vw;
        }

        @media screen and (max-width: $--screen-xs-min) {
            position: static;
            margin-bottom: 10px;
            height: calc(91.4vw * 0.55);
        }

        &:nth-child(2n-1) {
            grid-column: 1/6;

            // @media screen and (max-width: $--screen-md-min) {
            //     grid-column: 1/6;
            // }

            @media screen and (max-width: $--screen-sm-min) {
                grid-column: 1/7;
            }

            @media screen and (max-width: $--screen-xs-min) {
                grid-column: 1/10;
            }
        }

        &:nth-child(2n) {
            grid-column: 5/10;

            // @media screen and (max-width: $--screen-md-min) {
            //     grid-column: 5/10;
            // }

            @media screen and (max-width: $--screen-sm-min) {
                grid-column: 4/10;
            }

            @media screen and (max-width: $--screen-xs-min) {
                grid-column: 1/10;
            }
        }

        &__inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
        }

        &__front,
        &__back {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 20px;
            padding: 10px;
        }

        &__front {
            background-color: $--main-white;
        }

        &__back {
            top: -2px;
            bottom: -2px;
            left: -2px;
            right: -2px;
            opacity: 0;
            background-color: $--yellow-primary;
            border: 2px solid $--main-gray;
            padding: 10px;

            p {
                max-width: 462px;
                margin: auto;
            }
        }

        small {
            position: absolute;
            top: 20px;
            left: 10px;
            right: 10px;
            text-align: center;

            @media screen and (max-width: $--screen-md-min) {
                font-size: .875rem;
            }
        }

        &:hover {
            z-index: 2;

            .card-item__back {
                animation: fadein .3s ease forwards;
                border-color: $--main-black;
            }
        }

    }
</style>