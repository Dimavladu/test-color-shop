<template>
  <div class="card">
    <div class="card_img">
      <img :src="require(`../assets/colors/${item.img}`)" alt="" />
    </div>
    <div class="card_text">
      {{ item.name }}{{ item.mark }}, {{ item.color }} {{ item.unicname }}
      {{ item.id }}
    </div>
    <div class="card_info">
      <div class="card_info_price">{{ item.price }} ₽</div>
      <div class="card_info_btn" @click="$emit('addCard', item)">
        <plus-svg :stroke="'black'" class="plus" />
      </div>
    </div>
  </div>
</template>

<script>
import plusSvg from "./svg/plus.vue";

export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  emits: ["addCard"],
  components: { plusSvg },
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.card {
  width: 250px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  transition: 0.3s all ease;
  @media (max-width: 1366px) {
    width: 200px;
  }
  @media (max-width: 600px) {
    width: 150px;
  }
  &:hover {
    border-bottom: 1px solid rgba(0, 0, 0, 0.3);
  }
  &_img {
    display: flex;
    align-items: center;
    flex-direction: column;
    padding: 30px;

    @media (max-width: 1366px) {
      padding: 0 5%;
      img {
        height: 150px;
      }
    }
    @media (max-width: 1000px) {
      padding: 0;
    }
    @media (max-width: 600px) {
      img {
        height: 130px;
      }
    }
  }
  &_text {
    margin: 15px 0px 24px 0px;
    font-weight: 300;
    font-size: 16px;
    line-height: 112%;
    letter-spacing: 0.02em;
    color: #1f2020;
    @media (max-width: 1366px) {
      font-size: 14px;
    }
  }
  &_info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-bottom: 14px;
    &_price {
      font-weight: 600;
      font-size: 16px;
      line-height: 100%;
      color: #1f2020;
    }
    &_btn {
      cursor: pointer;
      background: #fff;
      border-radius: 8px;
      padding: 6px 30px;
      transition: 0.4s all ease;
      &:hover {
        background: #7bb899;
        .plus > * {
          stroke: #000;
        }
      }
    }
  }
}
</style>