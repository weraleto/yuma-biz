<template>
  <div class="navigation-link__dropdown" :class="{'opened': dropdownOpened,}">
        <div class="dropdown__header"
            :class="{'active': dropdownOpened || isDropdownActive}"
             @click="dropdownOpened=!dropdownOpened">
            <span class="dropdown__selected-title text4">
                <span class="dropdown__selected-title__text">{{title}}</span>
                <svg width="10" height="5" viewBox="0 0 10 5" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M0 0L5 5L10 0H0Z" fill="#111111"/>
                </svg>
            </span>
            
        </div>
        <div class="dropdown__items">
            <template v-if="showContacts">
                <div style="margin-bottom: 20px" class="dropdown__item">
                    <h3 class="text6" style="margin-bottom: 4px">Офис в Санкт-Петербурге</h3>
                    <a class="title3" href="tel:+7 (812) 309 50 32">+7 (812) 309 50 32</a>
                </div>
                <div class="dropdown__item">
                    <h3 class="text6" style="margin-bottom: 4px">Офис в Москве</h3>
                    <a class="title3" href="tel:+7 (495) 108 11 78">+7 (495) 108 11 78</a>
                </div>
            </template>
            <template v-else>
                <a :href="link.path" v-for="link in items" :key="link.name" class="dropdown__item"
                    :class="{'active': $route.path == link.path}"
                    >{{link.name}}</a>
            </template>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            default: ''
        },
        items: {
            type: Array,
            default: () => {}
        },
        menuOpened: {
            type: Boolean,
            default: false
        },
        showContacts: {
            type: Boolean,
            default: false
        },
    },
    data: () => {
        return {
            dropdownOpened: false
        }
    },
    methods: {
        requestDropdownClose() {
            const ctx = this
            setTimeout(()=>{
                ctx.dropdownOpened = false
            }, 2000)
        }
    },
    computed: {
        isDropdownActive() {
            return this.items.some(it=>it.path == this.$route.path)
        }
    },
    watch: {
        menuOpened() {
            if (!this.menuOpened) {
                this.dropdownOpened = false
            }
        }
    }
}
</script>

<style lang="scss" scoped>

@import '@/assets/scss/_variables.scss';

.navigation {
    &-link__dropdown {
        cursor: pointer;
        position: relative;
        display: flex;
        align-items: center;
        justify-content: space-between;
        background-color: white;

        @media screen and (max-width: $--screen-sm-min) {
            min-width: 100%;
            flex-direction: column;
        }
    }
}

.dropdown__header {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    position: relative;
    z-index: 10000;
    min-height: 68px;
    background-color: white;
    width: 100%;
    &.active {
        .dropdown__selected-title__text::after {
            opacity: 1;
        }
    }
    @media screen and (max-width: $--screen-sm-min) {
        padding: 0;
        min-height: unset;
        justify-content: flex-start;
    }
}
.dropdown__selected-title {
    display: flex;
    align-items: center;
    svg {
        margin-left: 8px;
    }
    &__text {
        position: relative;
        display: block;
        &::after {
            content: '';
            position: absolute;
            display: block;
            height: 3px;
            background-color: $--main-black;
            bottom: 0;
            left: 0;
            right: 0;
            opacity: 0;
            transform: translate(0, 8px);
            transition: opacity .3s ease;
        }
    }
}
.dropdown__items {
    position: absolute;
    top: calc(100% - 1px);
    left: 0;
    background-color: $--main-white;
    border-radius: 12px;
    padding: 16px;
    opacity: 0;
    white-space: pre-line;
    z-index: -1;
    visibility: hidden;
    transform: translate(0, -100px);
    transition: all .3s ease;
    @media screen and (min-width: calc($--screen-sm-min + 1px)) {
        box-shadow: 0px 8px 60px rgba(46, 46, 46, 0.1);
    }
    @media screen and (max-width: $--screen-sm-min) {
        display: flex;
        flex-direction: column;
        position: static;
        max-height: 0;
        overflow: hidden;
        transform: none;
        padding: 0;
        min-width: 100%;
        margin-bottom: 0;
    }
}
.navigation-link__dropdown.opened {
    .dropdown__items {
        z-index: 9999;
        visibility: visible;
        opacity: 1;
        transform: translate(0, 12px);

        @media screen and (max-width: $--screen-md-min) {
            max-height: 500px;
            padding-left: 16px;
            margin-bottom: 20px;
            padding-top: 10px;
        }
    }
}
.dropdown__item {
    position: relative;
    display: inline-block;
    white-space: nowrap;
    &:not(:last-child) {
        margin-bottom: 10px;
    }
    &::after {
        content: '';
        display: block;
        height: 2px;
        left: 0;
        right: 0;
        background-color: $--main-black;
        bottom: 0;
        transform: translate(0, 2px);
        opacity: 0;
        transition: opacity .3s ease;
    }
    &.active, &:hover {
        @media screen and (min-width: calc($--screen-sm-min + 1px)) {
            &::after {
                opacity: 1;
            }
        }
    }
}
</style>