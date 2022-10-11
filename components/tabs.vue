<template>
    <div class="tabs-wrapper">
        <el-tabs v-model="activeName" :id="id">
            <el-tab-pane :label="tab.label" :name="String(i)" v-for="(tab, i) in tabsContent" :key="tab.label">
                <div :class="`tab-content tab-content--${tab.type}`">
                    <div :class="`tab-picture tab-picture--${tab.type}`">
                        <img :src="require(`../assets/img/${imageFolderName}/${tab.img}`)" alt="Рестораны, бары">
                    </div>
                    <div :class="`tabs-swiper__container--${tab.type}`">
                        <client-only>
                            <swiper ref="tabsSwiper" 
                                class="swiper tabs-swiper" 
                                :options="getSwiperConfiguration(tab.type, String(i))"
                            >   
                                <swiper-slide 
                                    v-for="(slide, idx) in tab.slides" :key="idx"
                                    class="swiper-slide tabs-swiper__slide" 
                                    :class="`tabs-swiper__slide--${tab.type}`"
                                >
                                    <template v-if="tab.type == 'horizontal'">
                                        <h3 class="text4">{{slide.title}}</h3>
                                        <p class="text6">{{slide.text}}</p>
                                    </template>
                                    <template v-else>
                                        <div v-for="block in slide" :key="block.title" class="tabs-swiper__slide--block">
                                            <h3 class="text4">{{block.title}}</h3>
                                            <p class="text6">{{block.text}}</p>
                                        </div>
                                    </template>
                                </swiper-slide>
                            </swiper>
                        </client-only>
                    </div>
                </div>
                <div class="container" :class="`tabs-swiper__navigation tabs-swiper__navigation--${tab.type}`">
                    <div class="tabs-swiper__navigation--item"
                        :class="`tabs-swiper__navigation--prev-${String(i)}`"
                    >
                        <img src="~assets/img/swiper-arrow-prev.svg" alt="previous slide">
                    </div>
                    <div class="tabs-swiper__navigation--item"
                        :class="`tabs-swiper__navigation--next-${String(i)}`"
                    >
                        <img src="~assets/img/swiper-arrow-next.svg" alt="next slide">
                    </div>
                </div>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script>
    import ElTabs from 'element-ui/lib/tabs'
    import ElTabPane from 'element-ui/lib/tab-pane'
    import {
        Swiper,
        SwiperSlide
    } from 'vue-awesome-swiper'
    export default {
        props: {
            imageFolderName: String,
            id: String
        },
        components: {
            ElTabs,
            ElTabPane,
            Swiper,
            SwiperSlide
        },
        data: () => {
            return {
                activeName: '0',
                timer: null,
                swiperOptionsHorizontal: {
                    slidesPerView: 3,
                    slidesPerGroup: 3,
                    spaceBetween: 40,
                    breakpointsBase: 'container',
                    breakpoints: {
                        0: {
                            enabled: false,
                            allowTouchMove: false,
                            allowSlideChange: false,
                        },
                        768: {
                            enabled: true,
                            allowTouchMove: true,
                            allowSlideChange: true
                        }
                    }
                },
                swiperOptionsVertical: {
                    slidesPerView: 1,
                    slidesPerGroup: 1,
                    spaceBetween: 40,
                    breakpointsBase: 'container',
                    breakpoints: {
                        0: {
                            enabled: false,
                            allowTouchMove: false,
                            allowSlideChange: false,
                        },
                        768: {
                            enabled: true,
                            allowTouchMove: true,
                            allowSlideChange: true
                        }
                    }
                },
                tabsContent: [{
                    label: 'Рестораны, бары',
                    type: 'horizontal',
                    img: 'rest.jpg',
                    slides: [{
                            title: 'Предварительные заказы и бронирование онлайн',
                            text: 'В вашем приложении и на сайте гости смогут сами бронировать столики, видя реальную загрузку. А также заранее заказывать подачу блюд к удобному часу.'
                        },
                        {
                            title: 'Электронное и QR-меню',
                            text: 'Гостям за столиками не обязательно ждать официанта. Они могут самостоятельно делать заказы в мобильном приложении и на сайте.'
                        },
                        {
                            title: 'Приложение для официантов',
                            text: 'Официанты могут забивать заказы даже на планшетах и телефонах Android. Там же будут мгновенные уведомления о готовности блюд и функция распознавания постоянных клиентов по QR.'
                        },
                        {
                            title: 'Удобный расчёт с гостями',
                            text: 'Вы сможете принимать оплату деньгами и баллами лояльности. А также совмещать несколько типов оплаты и разделять счёт между гостями.'
                        },
                        {
                            title: 'Качество блюд и сервиса',
                            text: 'Фирменную рецептуру легко соблюдать благодаря безлимитным техкартам с модификаторами. А курсы подачи блюд помогут улучшить процесс обслуживания.'
                        },
                        {
                            title: 'Спецпредложения по меню',
                            text: 'По вашему желанию можно создать специальное меню, например, для завтрака в определённые часы.'
                        }
                    ]
                }, {
                    label: 'Кафе',
                    type: 'vertical',
                    img: 'cafe.jpg',
                    slides: [[{
                            title: 'QR-меню и онлайн-заказы',
                            text: 'С помощью QR-меню ваши гости смогут сами без кассира и официанта делать заказы прямо за столиком. В вашем мобильном приложении и на сайте им будет удобно заказывать доставку и самовывоз.'
                        },
                        {
                            title: 'Ускоряющий интерфейс кассы',
                            text: 'Интерфейс фронта кассира продуман и интуитивно понятен. По необходимости его можно дополнительно настроить под ваши персональные задачи.'
                        },
                        {
                            title: 'Киоски самообслуживания с электронной очередью',
                            text: 'Это стационарные терминалы, где покупатели могут делать заказы и оплачивать их без кассиров. Информация автоматически поступит на кухню, статусы готовности будут видны на фронте и в электронной очереди.'
                        }],
                        [{
                            title: 'Электронная реклама в заведениях',
                            text: 'На меню-бордах и экранах покупателей на кассах можно продвигать новые блюда, комбо-наборы и акции. Для этого достаточно через бэк-офис загрузить изображения и видеоролики, а затем настроить расписание показа.'
                        },
                        {
                            title: 'Конструктор блюд и комбо-наборов',
                            text: 'Безлимитные техкарты с модификаторами помогут вам создать разнообразное и гибкое меню. А ещё вы можете составлять выгодные комбо-наборы благодаря аналитике предпочтений и расчёту фудкоста в бэк-офисе.'
                        },
                        {
                            title: 'Безлимитная техподдержка',
                            text: 'Ваши сотрудники смогут решить вопросы в любое время по телефону и в мессенджерах. Бесплатно и без ограничений.'
                        }]
                    ]
                }, {
                    label: 'Пекарни, кофейни',
                    type: 'vertical',
                    img: 'bakery.jpg',
                    slides: [[{
                            title: 'Обслуживание нескольких покупателей одновременно',
                            text: 'Кассир может легко переключаться между заказами. Информация по каждому будет сохранена и доступна для дальнейшей работы до тех пор, пока заказ не будет завершён.'
                        },
                        {
                            title: 'Автоматические скидки',
                            text: 'Вы можете запускать любые акции и условия лояльности. Например, настроить скидку на выпечку и пирожные после 20.00, предлагать 7-й кофе в подарок и т.д.'
                        },
                        {
                            title: 'Весовой товар и продажа порциями',
                            text: 'Стоимость веса или части блюда будет рассчитываться автоматически благодаря гибким настройкам системы и полной интеграции весов.'
                        }],
                        [{
                            title: 'Удобный учёт ингредиентов и заготовок',
                            text: 'Количество ингредиентов для запланированного производства будет рассчитываться и списываться автоматически.'
                        },
                        {
                            title: 'Работа со складом и проведение инвентаризаций',
                            text: 'Вы сможете вести учёт, делать полные и частичные инвентаризации, работать с остатками, а также направлять заказы поставщикам.'
                        }]
                    ]
                }, {
                    label: 'Доставка',
                    type: 'horizontal',
                    img: 'delivery.jpg',
                    slides: [{
                            title: 'Собственное мобильное приложение и сайт для заказов',
                            text: 'Мы запустим их на одном ядре с системой автоматизации, поэтому меню, цены и акции будут загружаться и обновляться автоматически.'
                        },{
                            title: 'Управление всеми заказами через фронт кассира',
                            text: 'Заказы из колл-центра, мобильного приложения и с сайта отображаются в едином интерфейсе. Мы можем сделать интеграцию с Яндекс.Еда и Delivery Club, чтобы заказы с этих сервисов тоже приходили туда.'
                        },{
                            title: 'Организация работы вашего колл-центра',
                            text: 'Фронт кассира можно настроить для операторов колл-центра. Они смогут принимать звонки, определять постоянных покупателей и видеть их историю. А также видеть все заказы и их автоматическое распределение, либо самостоятельно распределять новые.'
                        },{
                            title: 'Удобное управление зонами доставки',
                            text: 'Они настраиваются прямо на карте в бэк-офисе. Для каждой зоны можно установить собственный режим работы и условия доставки.'
                        },{
                            title: 'Гибкие настройки условий заказов',
                            text: 'Например, можно задать минимальную сумму чека для доставки или самовывоза. Или стоимость, начиная с которой доставка будет бесплатной.',
                        },{
                            title: 'Построение работы собственных курьеров',
                            text: 'Наша система поддерживает две схемы работы. Вы можете назначать курьеров онлайн через фронт кассира. Или курьеры могут сами забирать заказы, сканируя их QR-коды в своём приложении.',
                        },{
                            title: 'Чёткий процесс выполнения заказов',
                            text: 'Заказ одним кликом передаётся с фронта кассира в приложение для кухни и сборки заказов. Готовый заказ автоматически распределяется на доставку или самовывоз. Заказ, назначенный на собственного курьера, сразу отображается у него в приложении для доставки.',
                        },{
                            title: 'Статусы заказов для покупателей',
                            text: 'При заказе в мобильном приложении и на сайте ваши покупатели увидят планируемое время доставки. А далее смогут отслеживать статусы исполнения: заказ готовится, готов, в пути.',
                        },{
                            title: 'Работа с отзывами',
                            text: 'Покупатели смогут оставлять отзывы в вашем приложении и на сайте. А вы по своему желанию опубликуете самые интересные и полезные из них.',
                        }
                    ]
                },{
                    label: 'Сети',
                    type: 'horizontal',
                    img: 'franshise.jpg',
                    slides: [
                        {
                            title: 'Мобильное приложение и сайт под брендом вашей сети', 
                            text: 'Ваши покупатели всегда смогут видеть актуальное меню, акции, отзывы и график работы каждого заведения. Они смогут делать заказы и пользоваться всеми привилегиями в режиме онлайн.'
                        },
                        {
                            title: 'Глобальная маркетинговая программа', 
                            text: 'В бэк-офисе вы сможете анализировать предпочтения своих гостей и запускать для них акции и условия лояльности. По вашему желанию они могут действовать только онлайн, в отдельных заведениях или всегда и по всей сети.'
                        },
                        {
                            title: 'Единый кабинет для управления всем бизнесом', 
                            text: 'Вы сможете управлять всеми заведениями, складами, перемещениями внутри сети и расчётами между владельцем франшизы и франчайзи с любого устройства, подключённого к интернету.'
                        },
                        {
                            title: 'Контроль работы каждого заведения и всей сети', 
                            text: 'Дашборд со сводными показателями покажет ключевые данные. А с помощью встроенной отчётности вы легко сможете получить необходимую глубокую аналитику.'
                        },
                        {
                            title: 'Лёгкий запуск новых точек в сети и франшизе', 
                            text: 'Экспорт меню и всех необходимых настроек поможет с быстрым стартом ваших новых заведений.'
                        },
                        {
                            title: 'Политика бренда и управление правами', 
                            text: 'Вы легко сможете внедрить единые стандарты и задать права для заведений сети или ваших франчайзи. Например, ввести единое меню и запретить его изменять.'
                        },
                        {
                            title: 'Управление поставками по всей сети', 
                            text: 'В бэк-офисе вы сможете настроить систему запланированных поставок с производства по всем точкам.'
                        },
                        {
                            title: 'Корректный учёт в разных часовых поясах', 
                            text: 'Система поддерживает временные зоны, поэтому учёт и отчётность по периодам всегда будут корректны, даже если заведения вашей сети работают в разных часовых поясах.'
                        },
                        {
                            title: 'Бесплатное обучение сотрудников и франчайзи', 
                            text: 'Сразу после подключения наши специалисты удалённо обучат всем возможностям системы и помогут с базовыми настройками.'
                        }
                    ]
                },{
                    label: 'Столовые',
                    type: 'horizontal',
                    img: 'cantines.jpg',
                    slides: [
                        {
                            title: 'Планирование производства и учёт',
                            text: 'Количество ингредиентов для всех запланированных блюд будет рассчитываться и списываться автоматически по безлимитным техкартам. А также вы сможете контролировать фудкост и управлять производством. Например, смотреть остатки за смену, чтобы делать оперативные переработки.'
                        },
                        {
                            title: 'Меню по дням недели и часам',
                            text: 'В бэк-офисе вы легко сможете настроить меню для каждого дня недели. А также для отдельных часов, например, для времени завтрака, обеда и ужина.'
                        },
                        {
                            title: 'Удобная продажа на вес и порциями',
                            text: 'Стоимость любых блюд, включая весовые, будет автоматически расчитываться на кассе благодаря полной интеграции весов в систему.'
                        },
                        {
                            title: 'Ускоряющий интерфейс кассы',
                            text: 'Фронт кассира продуман для работы с потоком покупателей. А интеллектуальный офлайн-режим делает обслуживание ещё быстрее при любом качестве интернет-соединения.'
                        },
                        {
                            title: 'Работа с постоянными посетителями',
                            text: 'Скидки и другие привилегии постоянным гостям можно легко настроить в бэк-офисе. Отправляйте им из вашего мобильного приложения полезные пуш-уведомления, например, о меню на день или актуальных акциях. Благодаря этому гости будут чаще приходить именно к вам.'
                        },
                        {
                            title: 'Организация питания на предприятии или в бизнес-центре',
                            text: 'В бэк-офисе вы сможете настроить систему баллов для общих, групповых и даже индивидуальных условий компенсации питания. Гостей можно идентифицировать через мобильное приложение, по QR-коду, проксимити-карте и другим носителям.'
                        }
                    ]
                }, {
                    label: 'Фудтраки',
                    type: 'vertical',
                    img: 'foodtruck.jpg',
                    slides: [[{
                            title: 'Скорость работы с заказами',
                            text: 'Интерфейс кассы продуман для максимально быстрой обработки заказов. А для удобного процесса выдачи вы можете печатать номера заказов или имена клиентов на пречеках.'
                        },
                        {
                            title: 'Работа на смартфонах и планшетах',
                            text: 'Фронт кассира полноценно работает даже на планшетах и смартфонах Android. Делать приходы и инвентаризации можно там же. А списания происходят автоматически при продаже.'
                        },
                        {
                            title: 'Автосохранение информации в офлайн-режиме',
                            text: 'Фронт кассира будет быстро и чётко работать даже при отключении от интернета. Вся информация сохранится, и после восстановления соединения касса и бэк-офис мгновенно синхронизируются.'
                        }],
                        [{
                            title: 'Продажа товаров любого типа',
                            text: 'Вы легко внесёте в систему учёта как приготовленные по техкартам блюда с любым количеством модификаторов, так и готовые товары. При продаже в любом случае списание со склада будет автоматическим.'
                        },
                        {
                            title: 'Управление бизнесом из любой точки мира',
                            text: 'Все ключевые бизнес-процессы будут под вашим контролем в режиме онлайн и с любого устройства. В том числе, показатели финансов, учёта, работы персонала и маркетинга.'
                        },
                        {
                            title: 'Поддержка работы сети и франшизы',
                            text: 'В бэк-офисе вы легко сможете запускать работу новых точек и осуществлять управленческий и финансовый контроль над всей сетью и каждым отдельным заведением.'
                        }]
                    ]
                },{
                    label: 'Кальянные',
                    type: 'vertical',
                    img: 'hookah.jpg',
                    slides: [[{
                            title: 'Удобный учёт табака',
                            text: 'Табак добавляется в заказ прямо с весов, расчёт стоимости смеси и списание всех ингредиентов происходит автоматически. Достаточно отсканировать штрихкод с каждой упаковки и насыпать нужное количество.'
                        },
                        {
                            title: 'Интеграция с вашими весами или поставка весов в комплекте',
                            text: 'Наша система полностью готова к работе со специальными весами для табака. Мы интегрируем ваши или предложим решение «под ключ».'
                        }],
                        [{
                            title: 'Сохранение табачных миксов в истории гостя',
                            text: 'Вы легко сможете повторить понравившийся постоянному посетителю состав кальяна. Для идентификации гостя достаточно номера телефона.'
                        },
                        {
                            title: 'Гибкий ассортимент',
                            text: 'Вы сможете продавать кальяны, а также напитки и сопутствующие блюда в единой системе. Списание со склада для всех позиций будет автоматическим.'
                        }]
                    ]
                }],

            }
        },
        mounted() {
            let navEl = document.querySelector(`#${this.id} .el-tabs__nav-scroll`)
            // navEl.addEventListener('scroll', this.handleTabScroll)
            navEl.addEventListener('touchmove', this.handleTabScroll)
        },
        methods: {
            getSwiperConfiguration(type, idx) {
                let config = type == 'horizontal' ? this.swiperOptionsHorizontal : this.swiperOptionsVertical;
                return {
                    ...config,
                    navigation: {
                        prevEl: `.tabs-swiper__navigation--prev-${idx}`,
                        nextEl: `.tabs-swiper__navigation--next-${idx}`
                    }
                }
            },
            debounce(timeout = 100, callback){
                if(this.timer){
                    clearTimeout(this.timer)
                }
                this.timer = setTimeout(callback, timeout)
            },
            
            handleTabScroll(e) {
                const target = document.querySelector(`#${this.id} .el-tabs__nav-scroll`)
                let el = target.querySelector('.el-tabs__nav')
                let tr = el.style.transform.replace("translateX(", "").replace(")", "")
                if (target.scrollLeft == 0 && parseInt(tr) != 0) {
                    this.debounce(150, function(){
                        el.style.transform = "translateX(0px)"
                    })
                }
            },
        }
    }
</script>

<style lang="scss">
@import "~element-ui/packages/theme-chalk/src/tabs";
@import "~element-ui/packages/theme-chalk/src/tab-pane";
@import "~swiper/swiper";
@import '@/assets/scss/_mixins';
@import '@/assets/scss/_variables';
.tabs-wrapper {
    grid-column: 1/13;
}
.el-tabs__header {
    @include container;
    max-width: $--container-width-default;
}
.el-tabs__active-bar {
    background-color: $--main-black;
    height: 3px;
    &::before, &::after {
        content: '';
        position: absolute;
        top: 0;
        bottom: 0;
        background-color: $--main-black;
        width: 24px;
    }
    &::before {
        right: 100%;
    }
    &::after {
        left: 100%;
    }
}
.el-tabs__nav-wrap::after {
    height: 1px;
    background-color: #d9d9d9;
}
.el-tabs__nav-scroll {
    overflow-x: scroll;
    &::-webkit-scrollbar {
        width: 0;
        height: 0;
    }
}
.el-tabs__item {
    height: 52px;
    line-height: 52px;
    font-weight: 400;
    font-size: 18px;
    padding-left: 24px;
    padding-right: 24px;

    &.is-active {
        color: $--main-black;
        font-weight: 500;
    }
    &:hover {
        color: $--main-black;
    }
}
.el-tabs--top .el-tabs__item.is-top:nth-child(2) {
    padding-left: 24px;
}


.el-tabs__nav-wrap.is-scrollable {
    padding: 0;
}
.el-tabs__content {
    margin-top: 40px;

    @media screen and (max-width: $--screen-sm-min) {
        margin-top: 20px;
    }
}

.tab-picture {
    @include container;
    max-width: $--container-width-default;
    
    position: relative;
    padding: 0 !important;

    &--horizontal {
        margin-bottom: 40px;
    }
    &--vertical {
        flex: 1 0 65.63%;

       
        @media screen and (max-width: $--screen-md-min) {
            flex: 1 1 auto;
        }
    }
     @media screen and (max-width: $--screen-md-min) {
        max-height: 35vw;
        // min-height: 35vw;
        overflow: hidden;
        display: flex;
        align-items: center;
        justify-content: center;
        img {
            width: 100vw;
        }
    }

    @media screen and (max-width: $--screen-sm-min) {
        margin-bottom: 20px;
        max-height: 51.73vw;
        min-width: 100vw;

        &--horizontal img {
            height: 100%;
            width: auto;
        }
    }
}

.tab-content {
    &--vertical {
        @include container;
        max-width: $--container-width-default;

        display: flex;
        gap: 40px;

        @media screen and (max-width: $--screen-md-min) {
            flex-direction: column;
            align-items: center;
            padding: 0;
        }
        @media screen and (max-width: $--screen-sm-min) {
            gap: 0;
        }
    }
}

.tabs-swiper {
    min-height: 100%;
    // display: flex;
    &__slide {
        h3 {
            margin-bottom: 20px;
            @media screen and (max-width: $--screen-sm-min) {
                margin-bottom: 16px;
            }
        }
        &--vertical {
            display: flex;
            height: 100%;
            flex-direction: column;
            gap: 3.89vw;

            @media screen and (min-width: calc($--screen-sm-min + 1px)) and (max-width: $--screen-md-min) {
                flex-direction: row;
                gap: 0;
            }
            @media screen and (max-width: $--screen-sm-min) {
                gap: 40px;
            }
        }
        &--horizontal {
            @media screen and (max-width: $--screen-sm-min) {
                min-width: 100%;
            }
        }

        &--block {
            @media screen and (min-width: calc($--screen-sm-min + 1px)) and (max-width: $--screen-md-min) {
                flex: 1 0 33.333333%;
                &:not(:last-child) {
                    padding-right: 40px;
                }
            }
        }
    }
    &__container {
        &--horizontal, &--vertical {
            
            @include container;
            max-width: $--container-width-default;

            @media screen and (max-width: $--screen-sm-min) {
                .swiper-wrapper {
                    display: flex;
                    flex-direction: column;
                    gap: 40px;
                }
            }
        }
        &--vertical {           
            width: 100%;
            overflow: hidden;
            &, .swiper-wrapper {
                min-height: 100%;
                flex-grow: 1;
                height: auto;
            }
            
            @media screen and (min-width: calc($--screen-md-min + 1px)) {
                padding-left: 0 !important;
                padding-right: 0 !important;
            }
            @media screen and (max-width: $--screen-sm-min) {
                &, .swiper-wrapper {
                    height: 100%;
                }
            }
        }
    }
    &__navigation {
        width: 100%;
        display: flex;
        justify-content: flex-end;
        margin-top: 19px;
        gap: 24px;
        &--item {
            cursor: pointer;
            &.swiper-button-disabled {
                display: none;
            }
        }

        @media screen and (max-width: $--screen-sm-min) {
            display: none;
        }
    }
}
</style>