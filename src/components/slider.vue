<template>
  <div class="wrapper">
    <div
      class="carousel"
      :style="{
        'margin-left': `${-sliderWidth * sliderIndex}px`,
      }"
    >
      <slider-item
        v-for="item in sliderList"
        :key="item.id"
        :itemData="item"
        :sliderWidth="sliderWidth"
      />
    </div>
    <button
      class="btn btn_prev"
      @click="sliderIndex--"
      v-if="sliderIndex !== 0"
    >
      <arrow-svg :rotate="180" />
    </button>
    <button
      class="btn btn_next"
      @click="sliderIndex++"
      v-if="sliderIndex !== sliderList.length - 1"
    >
      <arrow-svg />
    </button>
    <div class="pagination">
      <dot-svg
        v-for="(dot, i) in sliderList"
        :key="dot.id"
        class="dot"
        :class="{ pagination_opacity: sliderIndex !== i }"
        @click="sliderIndex = i"
      />
    </div>
    <div class="menu">
      <div class="menu_text">Главная</div>
      <dot-svg class="dot" />
      <div class="menu_text">Продукты</div>
      <dot-svg class="dot" />
      <div class="menu_text">Краски</div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

import dotSvg from "./svg/dot.vue";
import sliderItem from "./sliderItem.vue";
import arrowSvg from "./svg/arrow.vue";
export default {
  props: {
    sliderList: {
      type: Array,
      required: true,
    },
    sliderWidth: {
      type: Number,
      required: false,
    },
  },
  components: { sliderItem, arrowSvg, dotSvg },
  setup() {
    const sliderIndex = ref(0);

    return { sliderIndex };
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  @media (max-width: 600px) {
    display: none;
  }
  overflow: hidden;
  margin: 0 auto;
  margin-top: 102px;
  position: relative;
  .carousel {
    transition: 0.6s all ease;
    display: flex;
  }
  .btn {
    z-index: 2;
    transform: translate(-50%, -50%);
    position: absolute;
    bottom: 160px;
    &_prev {
      left: 25%;
    }
    &_next {
      right: 25%;
    }
    text-decoration: none;
    border: none;
    background-color: transparent;
  }
  .menu {
    position: absolute;
    top: 32px;
    left: 64px;
    display: flex;
    align-items: center;
    &_text {
      font-weight: 400;
      font-size: 10px;
      line-height: 100%;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      color: #ffffff;
      opacity: 0.3;
      transition: 0.3s all ease;
      cursor: pointer;
      &:hover {
        opacity: 0.6;
      }
    }
    .dot {
      width: 3px;
      height: 3px;
      fill: #c4c4c4;
      opacity: 0.3;
      padding: 8px;
    }
  }
  .pagination {
    position: absolute;
    bottom: 39px;
    padding: 9px 20px;
    background: rgba(0, 0, 0, 0.4);
    border-radius: 16px;
    display: flex;
    transform: translate(-50%, -50%);
    z-index: 2;
    left: 50%;
    .dot {
      padding: 4px;
      transition: 0.6s all ease;
      cursor: pointer;
      &:hover {
        opacity: 0.6;
      }
    }
  }
}
.pagination_opacity {
  opacity: 0.2;
}
</style>