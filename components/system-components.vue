<template>
    <div class="sys-components__container grid-layout">
        <div v-for="(item, i) in data" :key="i"
            class="sys-components__item"
            :class="[`col-${item.colspan}`, `row-${item.rowspan}`]"
            @click="openPopoverCard"
            :data-idx="i"
        >
            <div class="sys-components__item--front">
                <h3 class="subtitle sys-components__item--front__title">{{item.title}}</h3>
                <p>{{item.frontText}}</p>
            </div>
        </div>
        <div class="sys-components__popover" 
            :class="{'is_active': activeEl, 'is_visible': visibleEl}"
            ref="popoverComponent"
        >
            <div class="sys-components__popover--content" :class="{'visible': contentVisible}">
                <div class="sys-components__popover--close" @click="hidePopoverCard"></div>
                <div class="sys-components__popover--heading">
                    <h4 class="subtitle">{{activeElData.title}}</h4>
                    <p class="text6">{{activeElData.description}}</p>
                </div>
                <template v-if="activeElData.tab">
                    <SwiperWithPic
                        :i="activeEl"
                        image-folder-name="components"
                        :tab="activeElData.tab"
                        :swiper-options="getSwiperConfiguration(activeElData.tab.type, activeEl)"
                        :picture-bordered="true"
                    />
                </template>
            </div>
        </div>
    </div>
</template>

<script>
import SwiperWithPic from '@/components/swiper-with-pic'

export default {
    props: {
        data: {
            type: Array,
            default: () => []
        },
    },
    data: () => {
        return {
            activeEl: null,
            visibleEl: null,
            contentVisible: false,
            params: [],
            swiperOptionsBase: {
                spaceBetween: 40,
                breakpointsBase: 'container',
                on: {
                    init: function() {
                        const ctx = this
                        setTimeout(()=>{
                            ctx.update()
                            ctx.updateSize()
                        }, 310)
                        
                    }
                }
            },
            swiperOptionsHorizontal: {
                breakpoints: {
                    0: {
                        enabled: false,
                        allowTouchMove: false,
                        allowSlideChange: false,
                    },
                    768: {
                        enabled: true,
                        allowTouchMove: true,
                        allowSlideChange: true,
                        slidesPerView: 1.5,
                        slidesPerGroup: 1
                    },
                    1024: {
                        slidesPerView: 3,
                        slidesPerGroup: 3,
                    }
                },
            },
            swiperOptionsVertical: {
                breakpoints: {
                    0: {
                        enabled: false,
                        allowTouchMove: false,
                        allowSlideChange: false,
                    },
                    768: {
                        enabled: true,
                        allowTouchMove: true,
                        allowSlideChange: true,
                        slidesPerView: 1,
                        slidesPerGroup: 1,
                        spaceBetween: 20
                    },
                },
            },
            swiperOptionsVerticalSmall: {
                breakpoints: {
                    0: {
                        enabled: false,
                        allowTouchMove: false,
                        allowSlideChange: false,
                    },
                    768: {
                        enabled: true,
                        allowTouchMove: true,
                        allowSlideChange: true,
                        slidesPerView: 1,
                        slidesPerGroup: 1,
                        spaceBetween: 20
                    },
                    1024: {
                        slidesPerView: 2,
                        slidesPerGroup: 2,
                        spaceBetween: 20
                    },
                    1380: {
                        slidesPerView: 2,
                        slidesPerGroup: 2,
                        spaceBetween: 40
                    }
                },
            },
        }
    },
    components: {SwiperWithPic},
    computed: {
        activeElData() {
            if (this.activeEl) {
                return this.data[this.activeEl]
            }
            return {}
        }
    },
    methods: {
        getSwiperConfiguration(type, idx) {
            let config = type == 'horizontal' ? this.swiperOptionsHorizontal : this.swiperOptionsVertical;
            if (this.data[idx].tab.pictureSize && this.data[idx].tab.pictureSize == 'small') {
                config = this.swiperOptionsVerticalSmall
            }
            return {
                ...this.swiperOptionsBase,
                ...config,
                navigation: {
                    prevEl: `.tabs-swiper__navigation--prev-${idx}`,
                    nextEl: `.tabs-swiper__navigation--next-${idx}`
                }
            }
        },
        openPopoverCard(e) {
            const el = e.target.closest('.sys-components__item')
            let popoverEl = this.$refs.popoverComponent
            this.setElProperty(popoverEl, 'top', el.offsetTop, 'px')
            this.setElProperty(popoverEl, 'left', el.offsetLeft, 'px')
            this.setElProperty(popoverEl, 'maxWidth', el.clientWidth+2, 'px')
            this.setElProperty(popoverEl, 'maxHeight', el.clientHeight+2, 'px')
            this.setElProperty(popoverEl, 'zIndex', 5)
            this.params = [el.offsetTop, el.offsetLeft, el.clientWidth+2, el.clientHeight+2]

            this.visibleEl = this.activeEl = el.dataset.idx

            setTimeout(()=>{
                this.setElProperty(popoverEl, 'maxHeight', el.parentElement.clientHeight+2, 'px')
                this.setElProperty(popoverEl, 'maxWidth', el.parentElement.clientWidth+2, 'px')
                this.setElProperty(popoverEl, 'top', 0, 'px')
                this.setElProperty(popoverEl, 'left', 0, 'px')
            }, 100)
            setTimeout(()=>{
                this.contentVisible = true
            }, 200)
        },
        hidePopoverCard(e) {
            let [top, left, width, height] = this.params
            let popoverEl = this.$refs.popoverComponent
            this.contentVisible = false
            this.setElProperty(popoverEl, 'top', top, 'px')
            this.setElProperty(popoverEl, 'left', left, 'px')
            this.setElProperty(popoverEl, 'maxWidth', width, 'px')
            this.setElProperty(popoverEl, 'maxHeight', height, 'px')
            this.params = []
                        
            setTimeout(()=>{
                this.activeEl = null
            }, 200)
            setTimeout(()=>{
                this.visibleEl = null
                this.setElProperty(popoverEl, 'zIndex', -1)
            }, 250)
        },
        setElProperty(el, prop, val, units='') {
            el.style[prop] = `${val}${units}`
        }
    }
}
</script>

<style lang="scss">
@import '@/assets/scss/_variables';

.sys-components {
    &__container {
        gap: 20px;
        grid-auto-flow: column dense;
        grid-template-rows: repeat(3, 240px);
        position: relative;

        @media screen and (max-width: $--screen-md-min) {
            grid-template-columns: repeat(6, 1fr);
            grid-template-rows: repeat(5, 150px);
            grid-auto-flow: row dense;
            gap: 16px;
        }
        @media screen and (max-width: $--screen-xxs-min) {
            gap: 12px;
            grid-template-rows: 168px 278px 168px 278px 168px;
        }
    }

    &__popover {
        position: absolute;
        background: white;
        top: 0;
        left: 0;
        border-radius: $--products-default-border-radius;
        border: 1px solid $--gray-medium;
        width: 100%;
        height: 100%;
        max-width: 0;
        max-height: 0;
        overflow: hidden;
        z-index: -1;
        opacity: 0;
        transition: opacity .2s ease-in, z-index .2s ease-in;

        &.is_visible {
            opacity: 1;
        }

        &.is_active {
            padding: 40px;
            transition: all .2s ease-in;
        }

        &--close {
            position: absolute;
            width: 20px;
            height: 20px;
            background: url('~assets/img/cross.svg') no-repeat center center;
            background-size: cover;
            top: 42px;
            right: 42px;
            cursor: pointer;
            transition: all .3s ease;

            &:hover {
                transform: scale(1.15);
            }
        }

        &--heading {
            display: flex;
            flex-direction: column;
            gap: 12px;
            max-width: 471px;
            margin-bottom: 32px;
        }
        &--content {
            opacity: 0;
            transition: opacity .2s ease-in-out;
            &.visible {
                opacity: 1;
            }
        }

        @media screen and (max-width: $--screen-lg-min) {
            &.is_active {
                padding: 20px;
            }
            &--close {
                top: 20px;
                right: 20px;
            }
        }
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
            z-index: 1;
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
        &[data-idx="6"] {
            order: 10;
        }
        &--front {
            &__title {
                margin-bottom: 12px;
            }
        }

        @media screen and (max-width: $--screen-lg-min) {
            padding: 20px;   

            &::after {
                bottom: 20px;
                right: 20px;
            }
            &--front {
                .subtitle {
                    font-weight: 500;
                }
            }
        }
        @media screen and (max-width: $--screen-md-min) {
            &.row-2 {
                grid-row: span 1;
            }
        }
        @media screen and (max-width: $--screen-xs-min) {
            &[data-idx="4"] {
                order: 9;
            }
            &[data-idx="2"] {
                order: 8;
                grid-column: span 3;
            }
            &[data-idx="5"] {
                order: 7;
                grid-column: span 6;
            }
        }
        @media screen and (max-width: 330px) {
            padding: 10px;

            &::after {
                bottom: 10px;
                right: 10px;
            }
        }
    }

    .tab-picture--horizontal {
        margin-bottom: 32px;
    }

    .tabs-swiper__navigation {
        width: auto;
        @media screen and (min-width: 1024px) {
            z-index: 3;
            position: absolute;
            margin-top: 10px;
            right: 40px;
            bottom: 40px;
        }
    }

    .tab-picture {
        picture, img {
            height: 100%;
            width: 100%;
            object-fit: cover;
        }
    }
    .size-reverse-vertical {
        align-items: center;
        .tab-picture {
            &--vertical {
                flex: 1 0 31.25%;
                height: 560px;
            }
        }
    }
    .tab-content--vertical {
        @media screen and (max-width: $--screen-lg-min) {
            gap: 20px;
            .tabs-swiper {
                &__slide {
                    &--vertical {
                        gap: 20px;
                    }
                }
            }
            
        }
        @media screen and (max-width: $--screen-md-min) {
            flex-direction: row;
            .tab-picture {
                &--vertical {
                    height: 392px;
                }
            }
        }
        @media screen and (min-width: calc($--screen-sm-min + 1px)) and (max-width: $--screen-md-min) {
            .tabs-swiper {
                &__slide {
                    &--vertical {
                        flex-direction: column;
                    }
                    &--block {
                        flex: 1 1 100%;
                    }
                }
            }
        }
    }
}

</style>