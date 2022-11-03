<template>
  <div class="navigation-link__dropdown" :class="{'opened': dropdownOpened}">
        <div class="dropdown__header navigation-link__item"
            :class="{'active': dropdownOpened}"
             @click="dropdownOpened=!dropdownOpened">
            <span class="dropdown__selected-title text4">{{title}}
                <svg width="10" height="5" viewBox="0 0 10 5" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M0 0L5 5L10 0H0Z" fill="#111111"/>
                </svg>
            </span>
            
        </div>
        <div class="dropdown__items">
            <a :href="link.path" v-for="link in items" :key="link.name" class="dropdown__item"
                :class="{'active': $route.path == link.path}"
                >{{link.name}}</a>
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
        }
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
        // min-width: 220px;
        // min-width: 180px;
        
        display: flex;
        align-items: center;
        justify-content: space-between;
        background-color: white;
        // @media screen and (max-width: $--screen-lg-min) {
        //     min-width: 205px;
        // }
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
}
.dropdown__items {
    position: absolute;
    top: calc(100% - 1px);
    left: 0;
    background-color: $--main-white;
    border-radius: 12px;
    padding: 16px;
    opacity: 0;
    // min-width: 217px;
    z-index: -1;
    visibility: hidden;
    transform: translate(0, -100px);
    transition: all .3s ease;
    @media screen and (max-width: $--screen-sm-min) {
        display: flex;
        flex-direction: column;
        position: static;
        max-height: 0;
        overflow: hidden;
        transform: none;
        padding: 0;
        // border: 2px solid;
        // border-radius: 10px;
        min-width: 100%;
        margin-bottom: 0;
    }
}
.navigation-link__dropdown.opened {
    // .dropdown__header {
    //     color: $--main-gray;
    // }
    .dropdown__items {
        z-index: 9999;
        visibility: visible;
        opacity: 1;
        // transform: none;
        transform: translate(0, 12px);
        @media screen and (max-width: $--screen-md-min) {
            max-height: 500px;
            padding-left: 16px;
            // padding: 15px;
            margin-bottom: 20px;
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