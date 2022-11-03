<template>
    <div>
        <nav class="navigation bar" :class="{'opened': mobileMenuOpened}">
            <div class="container navigation-container grid-layout">
                <div class="navigation-burger only-mobile" @click="mobileMenuOpened=true; activePopup='menu'">
                    <img src="../assets/img/menu.svg" alt="Открыть меню">
                </div>
                <YumaLogo />
                <div class="navigation-inner" :class="{'opened': mobileMenuOpened}">
                    <img class="navigation-mobile-close" @click="mobileMenuOpened=false" src="../assets/img/cross.svg" alt="Закрыть меню">
                    <template v-if="activePopup=='menu'">
                        <div class="navigation-part left">
                            <div v-for="(it, idx) in navItems" :key="idx">
                                <template v-if="it.is_dropdown">
                                    <NavDropdown :title="it.title" :items="it.items" :menu-opened="mobileMenuOpened" />
                                </template>
                                <template v-else>
                                    <NuxtLink @click.native="mobileMenuOpened=false" :to="it.path" class="navigation-link__item text4"><span>{{it.title}}</span></NuxtLink>
                                </template>
                            </div>
                        </div>
                    </template>
                    <template v-else>
                        <h3 class="subtitle" style="margin-bottom: 56px">Мы работаем по всей России</h3>
                        <div style="margin-bottom: 56px">
                            <h3 class="subtitle" style="margin-bottom: 8px">Офис в Санкт-Петербурге</h3>
                            <p class="text6" style="margin-bottom: 20px">
                                Наб. реки Смоленки, 5-7, Технопарк, офис 337, метро Василеостровская
                            </p>
                            <a class="title3" href="tel:+7 (812) 309 50 32">+7 (812) 309 50 32</a>
                        </div>
                        <div>
                            <h3 class="subtitle" style="margin-bottom: 8px">Офис в Москве</h3>
                            <p class="text6" style="margin-bottom: 20px">
                                Нововладыкинский проезд, 2 стр. 2, метро Владыкино
                            </p>
                            <a class="title3" href="tel:+7 (495) 108 11 78">+7 (495) 108 11 78</a>
                        </div>
                    </template>
                    <!-- <div class="navigation-part right">
                        <div class="navigation-btn"> -->
                            <!-- <a href="#" 
                                @click.prevent="mobileMenuOpened=false; $store.commit('setShowModal', {key: 'showContactForm', val: true})"
                            class="btn medium outlined">связаться с нами</a> -->
                            <!-- <a href="#" 
                                @click.prevent class="btn medium outlined">Войти</a>
                        </div>
                    </div> -->

                </div>
                <div class="navigation-burger only-mobile" @click="mobileMenuOpened=true; activePopup='contacts'">
                    <img src="../assets/img/nav-phone.svg" alt="Контакты">
                </div>
            </div>
        </nav>
        <div class="body-overlay" v-if="mobileMenuOpened" @click="mobileMenuOpened=false"></div>
    </div>
</template>

<script>
import YumaLogo from '@/components/logo'
import NavDropdown from '@/components/navbar-dropdown'
export default {
    components: {YumaLogo, NavDropdown},
    data: () => {
        return {
            mobileMenuOpened: false,
            activePopup: 'menu',
            navItems: [
                {
                    is_dropdown: true,
                    title: 'YUMA-POS',
                    items: [{path: '/', name: 'О системе'}, {path: '/products', name: 'Компоненты и цены'}]
                },
                {
                    is_dropdown: false,
                    title: 'О нас',
                    path: '/about'
                }
            ]
        }
    },
    mounted() {
        window.addEventListener('resize', () => {
            if (this.mobileMenuOpened) {
                this.mobileMenuOpened=false
                this.activePopup='menu'
            }
        })
    }

}
</script>

<style lang="scss">

@import '@/assets/scss/_variables.scss';

.navigation {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    background-color: #fff;
    border-bottom: 2px solid $--main-gray;
    z-index: 10000;

    &.opened {
        border-color: transparent;
    }

    &-mobile-close {
        width: 20px;
        height: 20px;
        position: absolute;
        right: 17px;
        top: 20px;
        @media screen and (min-width: calc($--screen-xs-min + 1px)) {
            display: none;
        }
    }

    &-container {
        align-items: center;

        @media screen and (max-width: $--screen-sm-min) {
            &.grid-layout {
                display: flex;
                justify-content: space-between;
            }
        }
    }

    &-part {
        display: flex;
        width: 100%;
        align-items: center;
        
        &.left {
            flex-grow: 1;
            gap: 52px;

            @media screen and (min-width: calc($--screen-xs-min + 1px)) {
                justify-content: flex-end;
            }
        }
        &.right {
            flex-shrink: 1;
            max-width: 123px;
        }
        @media screen and (max-width: $--screen-sm-min) {
            flex-direction: column;
            align-items: flex-start;
            width: 100%;

            &.left {
                gap: 20px;
            }

            &.right {
                padding-left: 0;
                margin-top: 10px;
            }
        }
        
    }

    &-inner {
        grid-column: 3/13;
        display: flex;
        align-items: center;
        gap: 6.46vw;

        @media screen and (max-width: $--screen-sm-min) {
            position: absolute;
            flex-wrap: wrap;
            
            flex-direction: column;
            justify-content: flex-start;
            align-items: flex-start;
            background-color: #fff;
            border-radius: 0 0 20px 20px;
            right: 50px;
            top: calc(100% - 1px);
            min-width: 222px;
            padding: 20px;

            z-index: -1;
            visibility: hidden;
            transform: translate(0, -150%);
            transition: all .3s ease;

            &.opened {
                z-index: 9999;
                visibility: visible;
                transform: none;
            }
        }
        @media screen and (min-width: 1025px) and (max-width: 1280px) {
            .text5 {
                font-size: 14px;
            }
        }
        @media screen and (max-width: $--screen-sm-min) {
            // right: 30px;
            border-bottom-left-radius: 0;
            right: auto;
            left: 0;
        }
        @media screen and (max-width: $--screen-xs-min) {
            right: 0;
            top: 0;
            border-bottom-right-radius: 0;
            min-height: 100vh;
            padding-top: 10vh;

        }
    }

    &-link__item {
        position: relative;
        display: flex;
        align-items: center;
        min-height: 70px;

        span {
            position: relative;
            // display: inline-block;

            &::after {
                content: '';
                position: absolute;
                display: block;
                height: 3px;
                background-color: $--main-black;
                bottom: 0;
                left: 0;
                right: 0;
                transform: translate(0, 8px);
                opacity: 0;
                transition: opacity .3s ease;
            }
        }

        &:hover, &.nuxt-link-exact-active {
            span::after {
                opacity: 1;
            }
        }
        &:active, &.nuxt-link-exact-active, &.active {
            span::after {
                opacity: 1;
            }
        }        

        @media screen and (max-width: $--screen-sm-min) {
            min-height: unset;
            margin-bottom: 20px;
        }
    }

    &-burger {
        width: 24px;
        height: 24px;

        @media screen and (max-width: $--screen-xxs-min) {
            margin-right: 0;
        }
    }

    &-btn {
        width: 100%;
        .btn {
            font-size: 18px;
        }
        // @media screen and (min-width: $--screen-md-min) {
        //     max-width: 123px;
        // }
        @media screen and (max-width: $--screen-sm-min) {
            flex-grow: 1;
            display: flex;
            align-items: flex-end;
            // margin-top: 37px;

            .btn {
                max-height: 48px;
            }
        }
    }
}


</style>