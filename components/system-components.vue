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
            </div>
        </div>
    </div>
</template>

<script>
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
            params: []
        }
    },
    computed: {
        activeElData() {
            if (this.activeEl) {
                return this.data[this.activeEl]
            }
            return {}
        }
    },
    methods: {
        openPopoverCard(e) {
            const el = e.target.closest('.sys-components__item')
            let popoverEl = this.$refs.popoverComponent
            this.setElProperty(popoverEl, 'top', el.offsetTop, 'px')
            this.setElProperty(popoverEl, 'left', el.offsetLeft, 'px')
            this.setElProperty(popoverEl, 'maxWidth', el.clientWidth+2, 'px')
            this.setElProperty(popoverEl, 'maxHeight', el.clientHeight+2, 'px')
            this.params = [el.offsetTop, el.offsetLeft, el.clientWidth+2, el.clientHeight+2]

            this.visibleEl = el.dataset.idx
            this.activeEl = el.dataset.idx
            // setTimeout(()=>{
            // }, 100)
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
            }, 250)
        },
        setElProperty(el, prop, val, units='') {
            el.style[prop] = `${val}${units}`
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_variables';

.sys-components {
    &__container {
        gap: 20px;
        grid-auto-flow: column dense;
        grid-template-rows: repeat(3, 240px);
        position: relative;
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
            z-index: 2;
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
            max-width: 375px;
            margin-bottom: 32px;
        }
        &--content {
            opacity: 0;
            transition: opacity .2s ease-in-out;
            &.visible {
                opacity: 1;
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

</style>