<template>
  <div class="slider_item" :style="`width:${sliderWidth}px`">
    <img :src="require(`../assets/slider/${itemData.img}`)" alt="" />
    <div class="item_content">
      <p class="item_content_title">{{ itemData.title }}</p>
      <p class="item_content_text">{{ itemData.text }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    itemData: {
      type: Object,
      required: true,
    },
    sliderWidth: {
      type: Number,
      required: false,
    },
  },
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.slider_item {
  width: 100%;
  position: relative;
  transition: 0.6s all ease;
  img {
    object-position: center 0;
  }
  .item_content {
    position: absolute;
    text-align: center;
    margin: 0 auto;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 1;
    width: 500px;
    &_title {
      z-index: 5;
      font-weight: 400;
      font-size: 72px;
      line-height: 88%;
      letter-spacing: -0.02em;
      color: #ffffff;
    }
    &_text {
      font-weight: 500;
      font-size: 16px;
      line-height: 130%;
      text-align: center;
      letter-spacing: 0.02em;
      color: #ffffff;
    }
  }
}
</style>