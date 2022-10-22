<template>
    <div class="tabs-wrapper tabs-swipered">
        <el-tabs v-model="activeName" :id="id">
            <el-tab-pane :label="tab.label" :name="String(i)" v-for="(tab, i) in tabsContent" :key="tab.label">
                <div :class="`tab-content tab-content--${tab.type}`">
                    <div :class="`tab-picture tab-picture--${tab.type}`">
                        <picture v-lazy-load>
                        <source media="(min-width:1440px)" :data-srcset="require(`../assets/img/${imageFolderName}/${tab.img}.jpg`)">
                        <source media="(min-width:990px)" :data-srcset="require(`../assets/img/${imageFolderName}/${tab.img}0.75.jpg`)">
                        <source media="(min-width:0px)" :data-srcset="require(`../assets/img/${imageFolderName}/${tab.img}0.5.jpg`)">
                        <img :data-src="require(`../assets/img/${imageFolderName}/${tab.img}.jpg`)" :alt="tab.label">
                        </picture>
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
                    <div class="tabs-swiper__navigation--item animate"
                        :class="`tabs-swiper__navigation--next-${String(i)}`"
                        @click="handleSlideFirstChange"
                    >
                        <img src="~assets/img/swiper-arrow-next.svg" alt="next slide">
                    </div>
                </div>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script>
    import { tabsMixin } from '@/mixins/mixins'
    import {
        Swiper,
        SwiperSlide
    } from 'vue-awesome-swiper'
    export default {
        mixins: [tabsMixin],
        props: {
            imageFolderName: String,
            tabsContent: {
                type: Array,
                default: () => []
            },
        },
        components: {
            Swiper,
            SwiperSlide
        },
        data: () => {
            return {
                swiperOptionsBase : {
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
                swiperOptionsHorizontal: {
                    slidesPerView: 3,
                    slidesPerGroup: 3,
                },
                swiperOptionsVertical: {
                    slidesPerView: 1,
                    slidesPerGroup: 1,
                },
            }
        },
        methods: {
            getSwiperConfiguration(type, idx) {
                let config = type == 'horizontal' ? this.swiperOptionsHorizontal : this.swiperOptionsVertical;
                return {
                    ...this.swiperOptionsBase,
                    ...config,
                    navigation: {
                        prevEl: `.tabs-swiper__navigation--prev-${idx}`,
                        nextEl: `.tabs-swiper__navigation--next-${idx}`
                    }
                }
            },
            handleSlideFirstChange(e) {
                let el = e.target.closest('.tabs-swiper__navigation--item')
                if (el.classList.contains('animate')) {
                    el.classList.remove('animate')
                }
            }
        }
    }
</script>

<style lang="scss">
@import "~swiper/swiper";
@import '@/assets/scss/_mixins';
@import '@/assets/scss/_variables';
@import '@/assets/scss/components/tabs';

@keyframes arrowNextFullTiming {
    0%, 33%, 49.5%, 66% {
        transform: translateX(0);
    }

    41.25%, 57.75% {
        transform: translateX(30%);
    }
}

.tabs-swipered {
    .el-tabs__header {
        @include container;
        max-width: $--container-width-default;
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
        overflow: hidden;
        display: flex;
        align-items: center;
        justify-content: center;
        img, picture, source {
            width: 100vw;
        }
    }

    @media screen and (max-width: $--screen-xs-min) {
        margin-bottom: 20px;
        max-height: 51.73vw;
        min-width: 100vw;

        &--horizontal {
            img, picture, source {
                height: 100%;
                width: auto;
            }
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
            &.animate {
                animation-name: arrowNextFullTiming;
                animation-duration: 4s;
                animation-timing-function: linear;
                animation-iteration-count: infinite;
            }
        }

        @media screen and (max-width: $--screen-sm-min) {
            display: none;
        }
    }
}
</style>