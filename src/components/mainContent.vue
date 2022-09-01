<template>
  <div class="main">
    <div class="main_content">
      <div class="checkboxes">
        <check-box @changeType="changeFilterList('new')">Новинки</check-box>
        <check-box @changeType="changeFilterList('exsist')"
          >Есть в наличии</check-box
        >
        <check-box @changeType="changeFilterList('contract')"
          >Контрактные</check-box
        >
        <check-box @changeType="changeFilterList('exclusive')"
          >Экслюзивные</check-box
        >
        <check-box @changeType="changeFilterList('sale')">Распродажа</check-box>
      </div>
      <div class="filter_list_modal" v-show="filterModalToggle">
        <div
          class="filter_list_modal_wrapper"
          @click="filterModalToggle = false"
        ></div>
        <div class="filter_list_modal_content">
          <div class="tag"><tag-svg /></div>
          <check-box @changeType="changeFilterList('new')">Новинки</check-box>
          <check-box @changeType="changeFilterList('exsist')"
            >Есть в наличии</check-box
          >
          <check-box @changeType="changeFilterList('contract')"
            >Контрактные</check-box
          >
          <check-box @changeType="changeFilterList('exclusive')"
            >Экслюзивные</check-box
          >
          <check-box @changeType="changeFilterList('sale')"
            >Распродажа</check-box
          >
        </div>
      </div>
      <div class="main_cards" v-if="colorItems.length">
        <div class="main_cards_header">
          <div class="filter_modal" @click="filterModalToggle = true">
            Фильтры
          </div>
          <div class="count_card">{{ colorItems.length }} товаров</div>
          <my-select @selectedValue="(val) => $emit('selectedValue', val)" />
        </div>
        <div class="cards">
          <the-card
            v-for="item in colorItems"
            :key="item.id"
            :item="item"
            @addCard="(cardItem) => $emit('addCard', cardItem)"
          />
        </div>
      </div>
      <div v-else>Таких товаров не найдено</div>
    </div>
  </div>
</template>
 
<script>
import theCard from "./theCard.vue";
import mySelect from "./mySelect.vue";
import checkBox from "./checkBox";
import { computed, ref } from "@vue/runtime-core";

import tagSvg from "./svg/tag.vue";
export default {
  props: {
    colorItems: {
      type: Array,
      required: false,
    },
    modelValue: {
      type: Array,
      required: true,
    },
  },
  emits: ["addCard", "selectedValue", "update:modelValue"],
  components: { checkBox, theCard, mySelect, tagSvg },
  setup(props, { emit }) {
    const filterModalToggle = ref(false);
    const typeFilterList = computed({
      get() {
        return props.modelValue;
      },
      set(val) {
        emit("update:modelValue", val);
      },
    });

    const changeFilterList = (type) => {
      if (typeFilterList.value.includes(type)) {
        const indexOfDelete = typeFilterList.value.indexOf(type);
        delete typeFilterList.value[indexOfDelete];
      } else {
        typeFilterList.value.push(type);
      }
    };
    return { typeFilterList, changeFilterList, filterModalToggle };
  },
};
</script>

<style lang="scss" scoped>
.main {
  @media (max-width: 600px) {
    margin-top: 60px;
  }
}
.main_content {
  display: flex;
  padding: 44px 64px 44px 64px;
  .checkboxes {
    @media (max-width: 1000px) {
      display: none;
    }
  }
  @media (max-width: 600px) {
    padding: 10px;
  }
  .filter_list_modal {
    position: fixed;
    &_wrapper {
      background: rgba(0, 0, 0, 0.5);
      width: 100%;
      height: 100%;
      position: fixed;
      top: 0;
      right: 0;
      height: 100%;
      overflow: auto;
    }
    &_content {
      border-radius: 15px 15px 0 0;
      position: fixed;
      bottom: 0;
      right: 50%;
      height: 30%;
      width: 100%;
      background: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      transform: translate(50%, 0);
      .tag {
        position: absolute;
        top: 0;
      }
    }
  }
}
.main_cards {
  padding: 44px 0px 44px 130px;
  width: 100%;
  @media (max-width: 1366px) {
    padding-left: 50px;
  }
  @media (max-width: 1000px) {
    padding-left: 10px 0;
  }
  @media (max-width: 600px) {
    margin-top: 60px;
    padding: 10px 5px;
  }
  &_header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-weight: 500;
    font-size: 12px;
    line-height: 15px;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    color: #1f2020;
    .count_card {
      @media (max-width: 1000px) {
        display: none;
      }
    }
    .filter_modal {
      display: none;
      @media (max-width: 1000px) {
        display: block;
        cursor: pointer;
      }
    }
    .sort_card {
    }
  }
  .cards {
    margin-top: 44px;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
  }
}
</style>