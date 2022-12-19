<template>
  <main class="main">
    <div class="container pb item-page">
      <Breadcrumbs
        :links="[
          {name: 'YUMA-SMART', to: {name: 'yuma-smart'}}, 
          {name: 'Тариф №3 Готовый микромаркет', to: {name: 'yuma-smart-slug', params: {slug: 'tariff3-integrated-micromarkets'}}},
          {name: itemData.name, to: {name: 'yuma-smart-integrated-micromarkets-slug', params: {slug: itemData.slug}}}
          ]"
      ></Breadcrumbs>
      <div class="item-page__wrapper">
        <div class="item-page__col">
          <h1 class="item-page__title title1 block-offset__title" v-html="itemData.name" />
          <div class="item-page__pic only-mobile">
            <img :src="require('/assets/img/smart/cata/'+imageName+'.png')" :alt="itemData.slug">
          </div>
          <div class="item-page__main-specs">
            <p class="text6">Тип: {{ itemData.type }}</p>
            <p class="text6">Литраж: {{ itemData.litres }} л</p>

            <div class="item-page__radio">
              <el-radio-group v-model="material">
                <el-radio :label="0">белый</el-radio>
                <el-radio :label="1">нерж. сталь</el-radio>
              </el-radio-group>
            </div>
            <div class="item-page__action">
              <div class="item-page__action--price">
                <h3 class="subtitle-bold">{{itemData.prices[material]}} ₽</h3>
                <span class="text5">+ 7% от оборота</span>
              </div>
              <button class="btn primary text4"
                @click.prevent="$store.commit('setShowModal', {key: 'showApplyForm', val: true})">Заказать</button>
            </div>
          </div>
          <div>
            <el-table :data="itemData.features" stripe :highlight-current-row="false" :fit="true">
              <el-table-column prop="prop_name" label="Характеристики" class-name="text-bold">
              </el-table-column>
              <el-table-column prop="prop_val" label="" >
              </el-table-column>
            </el-table>
          </div>
        </div>
        <div class="item-page__col hidden-mobile">
          <img :src="require('/assets/img/smart/cata/'+imageName+'.png')" :alt="itemData.slug">
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { yumaSmartCatalogue } from '@/assets/dataContent'
import ElTable from 'element-ui/lib/table'
import ElTableColumn from 'element-ui/lib/table-column'
import ElRadioGroup from 'element-ui/lib/radio-group'
import ElRadio from 'element-ui/lib/radio'
import Breadcrumbs from '@/components/breadcrumbs'
export default {
    components: {
        ElTable,
        ElTableColumn,
        ElRadioGroup,
        ElRadio,
        Breadcrumbs
    },
  data: () => {
    return {
      itemData: {},
      material: 0,
    }
  },
  asyncData({ params, error }) {
    const itemData = yumaSmartCatalogue.reduce((prev, next, i) => {
      return next.slug === params.slug ? next : prev
    }, {})
    if (!Object.keys(itemData).length) {
      error({ statusCode: 404, message: 'Страница не найдена' })
    }

    return { itemData }
  },
  computed: {
    materialName() {
      return this.material == 0 ? 'LW' : 'LS'
    },
    imageName() {
      let materialName = this.materialName
      if (this.itemData.is_frost) {
          materialName = 'LS'
      }
      return this.itemData.img + materialName.toLowerCase()
    }
  }
}
</script>

<style lang="scss">
@import '@/assets/scss/_variables.scss';

$--radio-checked-font-color: $--main-black;
$--color-text-regular: $--main-black;
$--radio-checked-input-border-color: $--yellow-hover;
$--radio-checked-icon-color: $--yellow-hover;
$--font-size-base: 1.125rem;
$--table-header-font-color: $--main-black;


@import "~element-ui/packages/theme-chalk/src/table";
@import "~element-ui/packages/theme-chalk/src/table-column";
@import "~element-ui/packages/theme-chalk/src/radio";
@import "~element-ui/packages/theme-chalk/src/radio-group";


.el-table .cell {
    word-break: normal;
}

.item-page {

  &__wrapper {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10.9vw;
    margin-top: 56px;
    @media screen and (max-width: $--screen-md-min) {
      gap: 30px;
    }
    @media screen and (max-width: $--screen-sm-min) {
      display: flex;
    }
  }

  &__col {
    @media screen and (max-width: $--screen-sm-min) {
      width: 100%;
    }
  }

  &__pic {
    width: 100%;
    max-width: 250px;
    margin-top: 8px;
  }

  &__action {
    display: flex;
    align-items: center;
    gap: 4.51vw;

    &--price {
      display: flex;
      flex-direction: column;
      gap: 8px;
       @media screen and (max-width: 360px) {
        min-width: 140px;
        transform: scale(.9) translateX(-5%);
       }
    }

    .btn {
      min-height: 60px;
      max-width: 157px;
    }

    @media screen and (max-width: $--screen-xs-min) {
      justify-content: space-between;
    }
  }

  &__radio {
    margin-top: 12px;
    margin-bottom: 24px;

    label {
      display: block;
      line-height: 40px;
    }
  }

  &__main-specs {
    margin: 16px 0 42px;
  }

  .el-table th.el-table__cell {
    padding-bottom: 24px;
    font-weight: 400;
  }
}
</style>