<template>
  <header class="header">
      <div class="container header__container">
        <h1>{{title}}</h1>
        <h2>{{subtitle}}</h2>
        <div class="header__promo">
          <div class="header__promo--text">
            <p v-for="(line, i) in buttonSubtext"
                :key="i"
                class="text4"
            >
                {{line}}
            </p>
          </div>
          <button class="btn primary large text4" 
                  @click.prevent="$store.commit('setShowModal', {key: 'showApplyForm', val: true})"
          >{{buttonText}}</button>
        </div>
      </div>
      <div class="header__top" :style="{'alignItems': pictureAlignment}">
        <slot />
      </div>
    </header>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            default: ''
        },
        subtitle: {
            type: String,
            default: ''
        },
        buttonSubtext: {
            type: Array,
            default: () => []
        },
        buttonText: {
            type: String,
            default: ''
        },
        pictureAlignment: {
          type: String,
          default: 'flex-end'
        }
    }
}
</script>

<style lang="scss">
@import '@/assets/scss/_variables';

.header {
    margin-bottom: 50px;
    h1 {
      font-size: 134px;
      text-transform: uppercase;
      font-weight: 800;
      margin-bottom: 24px;

      @media screen and (max-width: $--screen-lg-min) {
        font-size: 12.5vw;
      }
      @media screen and (max-width: $--screen-xs-min) {
        margin-bottom: 12px;
      }
    }

    h2 {
      font-weight: 500;
      font-size: 56px;
      text-transform: uppercase;

      @media screen and (max-width: $--screen-md-min) {
        font-size: 7.46vw;
        line-height: 1.42em;
      }
    }

    &__top {
      max-height: 70vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      position: relative;
      picture, img {
        height: 700px;
        width: 100%;
        object-fit: cover;

        @media screen and (max-width: 700px)  {
          height: auto;
          width: 100%;
        }
      }
      
    }

    &__container {
      padding-top: 110px;
      padding-bottom: 150px;
      @media screen and (max-width: $--screen-sm-min) {
        padding-bottom: 72px;
      }
      @media screen and (max-width: $--screen-xs-min) {
        padding-top: 32px;
      }
    }

    &__promo {
      margin: 60px auto 0;
      text-align: center;

      &--text {
        margin-bottom: 28px;
      }

      .btn {
        margin: auto;
      }
    }

    @media screen and (max-width: $--screen-xs-min) {
      margin-bottom: 32px;
    }
  }
</style>