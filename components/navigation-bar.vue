<template>
    <div>
        <nav class="navigation bar" :class="{'opened': mobileMenuOpened}">
            <div class="container navigation-container grid-layout">
                <div class="navigation-burger only-mobile" @click="mobileMenuOpened=!mobileMenuOpened; activePopup='contacts'">
                    <img src="../assets/img/nav-phone.svg" alt="Контакты">
                </div>
                <div class="navigation-inner right" :class="{'opened': mobileMenuOpened && activePopup=='menu'}">
                    <img class="navigation-mobile-close" @click="mobileMenuOpened=false" src="../assets/img/cross.svg" alt="Закрыть меню">
                    <div class="navigation-part left">
                        <template v-for="(it, idx) in navItems">
                            <template v-if="it.is_dropdown">
                                <NavDropdown :title="it.title" 
                                :key="idx"
                                :items="it.items || []" 
                                :menu-opened="mobileMenuOpened" 
                                :show-contacts="it.showContacts"
                                :class="it.class || ''"
                                :ref="`navDropdown-${idx}`"
                                @open="changeDropdownStatus(idx)"
                                @closemenu="mobileMenuOpened=false"
                                @click.stop
                            />
                            </template>
                            <template v-else>
                                <a :href="it.path" 
                                    :key="idx"
                                    class="navigation-link__item text4"
                                    :class="{'active': $route.path == it.path}"
                                    :target="it.external ? '_blank': '_self'"
                                ><span>{{it.title}}</span></a>
                            </template>
                        </template>
                    </div>
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
                <div class="navigation-inner left only-mobile" :class="{'opened': mobileMenuOpened && activePopup=='contacts'}">
                    <img class="navigation-mobile-close" @click="mobileMenuOpened=false" src="../assets/img/cross.svg" alt="Закрыть меню">

                    <h3 class="subtitle" style="margin-bottom: 8vh">Мы работаем по всей России</h3>
                    <div style="margin-bottom: 8vh">
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
                </div>
                <YumaLogo />
                <div class="navigation-burger only-mobile" @click="mobileMenuOpened=!mobileMenuOpened; activePopup='menu'">
                    <img src="../assets/img/menu.svg" alt="Открыть меню">
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
                },
                {
                    is_dropdown: false,
                    external: true,
                    title: 'Техподдержка',
                    path: 'https://support.yumapos.ru/'
                },
                {
                    is_dropdown: true,
                    title: 'Контакты',
                    showContacts: true,
                    class: 'hidden-mobile'
                },
            ],
            dropdownStatuses: {}
        }
    },
    mounted() {
        this.navItems.forEach((it, idx)=>{
            if (it.is_dropdown){
                this.dropdownStatuses[idx] = false
            }
        })
        window.addEventListener('resize', () => {
            if (this.mobileMenuOpened) {
                this.mobileMenuOpened=false
                this.activePopup='menu'
            }
        })
    },
    methods: {
        changeDropdownStatus(idx) {
            this.dropdownStatuses[idx] = true
            let activeDropdowns = Object.keys(this.dropdownStatuses).filter(
                key=>key != idx && this.dropdownStatuses[key]
            )
            if (activeDropdowns.length) {
                activeDropdowns.forEach(it=>{
                    this.$refs['navDropdown-'+it][0].requestDropdownClose()
                })
            }
        }
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
    z-index: 10000;
    box-shadow: 0px 8px 60px rgba(46, 46, 46, 0.1);

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
                & > div {
                    width: 100%;
                }
            }

            &.right {
                padding-left: 0;
                margin-top: 10px;
            }
        }
        
    }

    &-inner {
        grid-column: 1/12;
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
            top: calc(100% - 1px);
            min-width: 222px;
            padding: 20px;
            z-index: -1;
            visibility: hidden;
            
            transition: all .3s ease;

            &.left {
                right: auto;
                left: 0;
                transform: translate(-150%, 0%);
                border-radius: 0 0 20px 0;
            }

            &.right {
                left: auto;
                right: 0;
                transform: translate(150%, 0%);
                border-radius: 0 0 0 20px;
            }

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
        @media screen and (max-width: $--screen-xs-min) {
            &.left, &.right {
                left: 0;
                right: 0;
                top: 0;
                border-radius: 0;
            }
            min-height: 100vh;
            padding-top: 10vh;
        }
        @media screen and (max-width: $--screen-xxs-min) {
            .subtitle {
                font-size: 18px;
            }
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