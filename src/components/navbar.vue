<template>
  <div class="nav_bar">
    <burger-svg class="nav_bar_burger" />
    <div class="nav_bar_title">
      <img src="../assets/logo.jpg" alt="" />
    </div>
    <div class="nav_bar_pages">
      <div class="nav_bar_page">Продукты</div>
      <div class="nav_bar_page">Цвета</div>
      <div class="nav_bar_page">Вдохновение</div>
      <div class="nav_bar_page">Советы</div>
      <div class="nav_bar_page">Найти магазин</div>
    </div>
    <div class="nav_bar_contact">
      <div class="nav_bar_contact_phone">+7 (495) 221-77-69</div>
      <div class="nav_bar_contact_text">Заказать звонок</div>
    </div>
    <div class="nav_bar_icons">
      <div class="nav_bar_icon"><search-svg /></div>
      <div class="nav_bar_icon"><profile-svg /></div>
      <div class="nav_bar_icon"><heart-svg /></div>
      <div class="nav_bar_icon_cart" @click="changeModalVisible">
        {{ cartItems.length }}
      </div>
    </div>
    <modal
      :height="height"
      :cartItems="cartItems"
      @closeModal="changeModalVisible"
      v-show="modalToggle"
      @changeCartItems="(items) => $emit('changeCartItems', items)"
    />
  </div>
</template>

<script>
import burgerSvg from "./svg/navbar/burger.vue";
import searchSvg from "./svg/navbar/search.vue";
import profileSvg from "./svg/navbar/profile.vue";
import heartSvg from "./svg/navbar/heart.vue";
import dotSvg from "./svg/dot.vue";

import modal from "./modal.vue";

import { ref } from "@vue/reactivity";

export default {
  props: {
    cartItems: {
      type: Array,
      required: false,
    },
    height: {
      type: Number,
      required: true,
      default: () => 1000,
    },
  },
  emits: ["changeCartItems", "changeModalVisible"],
  components: {
    burgerSvg,
    dotSvg,
    searchSvg,
    profileSvg,
    heartSvg,
    modal,
  },
  setup(_, { emit }) {
    const modalToggle = ref(false);
    const burgerToggle = ref(true);

    const changeModalVisible = () => {
      modalToggle.value = !modalToggle.value;
      emit("changeModalVisible", modalToggle.value);
    };
    return { burgerToggle, modalToggle, changeModalVisible };
  },
};
</script>

<style lang="scss" scoped>
.nav_bar {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 4;
  width: 100%;
  background: #fff;
  font-style: "Inter";
  margin: 0px;
  padding: 35px 40px 35px 10px;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  &_burger {
    display: none;
    @media (max-width: 1000px) {
      display: block;
    }
  }
  &_title {
    font-family: "Hoves";
    display: flex;
    justify-content: start;
    font-weight: 400;
    font-size: 30px;
    line-height: 88%;
    color: #1f2020;
    &_dot {
      padding-top: 3%;
    }
  }
  &_pages {
    display: flex;
    align-items: center;
    gap: 24px;
    @media (max-width: 1000px) {
      display: none;
    }
  }
  &_page {
    font-weight: 400;
    font-size: 14px;
    line-height: 100%;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    color: #1f2020;
    transition: 0.3s all ease;
    cursor: pointer;
    &:hover {
      opacity: 0.5;
    }
    @media (max-width: 1366px) {
      font-size: 12px;
    }
  }
  &_contact {
    @media (max-width: 1000px) {
      display: none;
    }
  }
  &_contact_phone {
    font-weight: 500;
    line-height: 100%;
    font-size: 16px;
  }
  &_contact_text {
    font-weight: 400;
    font-size: 14px;
    line-height: 100%;
    color: #1f2020;
    opacity: 0.3;
  }
  &_icons {
    display: flex;
    gap: 24px;
  }
  &_icon {
    @media (max-width: 1000px) {
      display: none;
    }
    cursor: pointer;
    &_cart {
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 22px;
      width: 22px;
      background-color: #7bb899;
      border-radius: 15px;
      font-weight: 500;
      font-size: 12px;
      line-height: 15px;
      text-align: center;
      letter-spacing: 0.06em;
    }
  }
}
</style>