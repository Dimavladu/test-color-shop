<template>
  <div class="modal">
    <div class="modal_wrapper"></div>
    <div class="modal_cart" :style="`height: ${height}px`">
      <div class="modal_cart_wrapper">
        <div class="modal_cart_wrapper_header">
          <div class="modal_cart_wrapper_header_text">Корзина</div>
          <div
            class="modal_cart_wrapper_header_button"
            @click="$emit('closeModal')"
          >
            <close-svg />
          </div>
        </div>
        <div class="modal_cart_wrapper_body" v-if="listItems.length">
          <div class="modal_cart_wrapper_body_header">
            <div class="modal_cart_wrapper_body_header_count">
              {{ countNumber }} {{ countLetter }}
            </div>
            <div
              class="modal_cart_wrapper_body_header_clear"
              @click="listItems = []"
            >
              очистить список
            </div>
          </div>
        </div>
        <div class="modal_cart_wrapper_body_header" v-else>
          Ваша корзина пуста
        </div>

        <div
          class="modal_cart_wrapper_body_card"
          v-for="item in listItems"
          :key="item.id"
        >
          <div
            :style="item.count ? '' : 'opacity: 0.5'"
            class="modal_cart_wrapper_body_card_main"
          >
            <img
              class="modal_cart_wrapper_body_card_main_img"
              height="96"
              :src="require(`../assets/colors/${item.img}`)"
              alt=""
            />
            <div class="modal_cart_wrapper_body_card_main_text">
              <div class="modal_cart_body_card_main_text_name">
                {{ item.name }} {{ item.mark }}, {{ item.color }}
                {{ item.unicname }}
              </div>
              <div class="modal_cart_wrapper_body_card_main_text_price">
                {{ item.price }} ₽
              </div>
            </div>
            <div class="modal_cart_wrapper_body_card_main_buttons">
              <div
                class="modal_cart_wrapper_body_card_main_buttons_btn"
                @click="item.count ? item.count-- : item.count"
              >
                <minus-svg />
              </div>
              <div class="modal_cart_wrapper_body_card_main_buttons_text">
                {{ item.count }}
              </div>
              <div
                class="modal_cart_wrapper_body_card_main_buttons_btn"
                @click="item.count++"
              >
                <plus-svg :stroke="'black'" height="16px" width="16px" />
              </div>
            </div>
          </div>
          <close-svg
            v-if="item.count > 0"
            class="sub_close"
            @click="item.count = 0"
          />
          <repeat-svg
            v-else-if="item.count === 0"
            class="sub_repeat"
            @click="item.count++"
          />
        </div>
      </div>

      <div class="modal_cart_bottom" v-if="listItems.length">
        <div class="modal_cart_bottom_wrapper">
          <div class="modal_cart_bottom_wrapper_text">
            Итого
            <div class="modal_cart_bottom_wrapper_text_price">
              {{ sumPrice }} ₽
            </div>
          </div>
          <button class="modal_cart_bottom_wrapper_btn">оформить заказ</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from "@vue/runtime-core";

import closeSvg from "./svg/navbar/close.vue";
import plusSvg from "./svg/plus.vue";
import minusSvg from "./svg/minus.vue";
import repeatSvg from "./svg/repeat.vue";

export default {
  components: { closeSvg, plusSvg, minusSvg, repeatSvg },
  props: {
    cartItems: {
      type: Array,
      required: false,
      default: () => [],
    },
    height: {
      type: Number,
      required: true,
    },
  },
  emits: ["closeModal", "changeCartItems"],
  setup(props, { emit }) {
    const listItems = computed({
      get() {
        return props.cartItems;
      },
      set(items) {
        emit("changeCartItems", items);
      },
    });

    const countNumber = computed(() =>
      listItems.value.reduce((prev, next) => prev + next.count, 0)
    );
    const countLetter = computed(() => {
      let n = Math.abs(countNumber.value);
      n %= 100;
      if (n >= 5 && n <= 20) return "товаров";
      n %= 10;
      if (n === 1) return "товар";
      if (n >= 2 && n <= 4) return "товара";
      return "товаров";
    });
    const sumPrice = computed(() => {
      if (listItems.value.length) {
        return listItems.value.reduce(
          (prev, next) => prev + next.price * next.count,
          0
        );
      } else {
        return 0;
      }
    });
    return { countNumber, countLetter, sumPrice, listItems };
  },
};
</script>

<style lang="scss" scoped>
img {
  height: 100px;
}
.modal {
  position: fixed;

  &_wrapper {
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    right: 0;
    height: 100%;
  }
  &_cart {
    position: fixed;
    top: 0;
    right: 0;
    width: 30%;
    background: #fff;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    @media (max-width: 600px) {
      width: 100%;
    }
    &_wrapper {
      overflow: auto;

      padding: 32px;
      @media (max-width: 1366px) {
        padding: 20px;
      }
      &_header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 80px;
        &_text {
          padding: 0;
          font-weight: 500;
          font-size: 30px;
          line-height: 88%;
          letter-spacing: -0.04em;
          color: #1f2020;
        }
        &_button {
          cursor: pointer;
          padding: 15px;
          border: 1px solid rgba(0, 0, 0, 0.1);
          border-radius: 50px;
          display: flex;
          align-items: center;
          transition: 0.3s all ease;
          &:hover {
            background: #f2f2f2;
            opacity: 0.5;
          }
        }
      }
      &_body {
        &_header {
          display: flex;
          align-items: center;
          justify-content: space-between;
          padding: 10px 0;
          &_clear {
            cursor: pointer;
            font-weight: 300;
            font-size: 14px;
            line-height: 112%;
            color: #1f2020;
            opacity: 0.4;
            transition: 0.3s all ease;
            &:hover {
              opacity: 0.7;
            }
          }
        }
        &_card {
          display: flex;
          align-items: center;
          width: 100%;
          border-top: 1px solid rgba(0, 0, 0, 0.1);
          height: 120px;
          justify-content: space-between;
          &_main {
            width: 90%;
            display: flex;
            align-items: center;
            justify-content: space-between;
            &_img {
              padding-bottom: 15px;
            }
            &_text {
              width: 170px;
              display: flex;
              flex-direction: column;
              gap: 16px;
              @media (max-width: 1366px) {
                font-size: 14px;
              }
              &_price {
                font-weight: 600;
                font-size: 16px;
                line-height: 100%;
                color: #1f2020;
              }
            }
            &_buttons {
              display: flex;
              align-items: center;
              gap: 21px;
              @media (max-width: 1366px) {
                gap: 10px;
              }
              &_btn {
                cursor: pointer;
                display: flex;
                justify-content: center;
                align-items: center;
                border-radius: 4px;
                width: 40px;
                height: 24px;
                background: #f2f2f2;
                transition: 0.3s all ease;
                @media (max-width: 1366px) {
                  width: 30px;
                  height: 20px;
                }
                &:hover {
                  opacity: 0.6;
                }
              }
            }
          }
        }
      }
    }
    &_bottom {
      padding: 32px;
      &_wrapper {
        display: flex;
        justify-content: space-between;
        align-items: bottom;
        &_text {
          &_price {
            font-weight: 500;
            font-size: 30px;
            line-height: 100%;
            letter-spacing: -0.02em;
            color: #1f2020;
          }
        }
        &_btn {
          font-family: "Inter";
          font-weight: 500;
          font-size: 12px;
          line-height: 15px;
          text-align: center;
          letter-spacing: 0.06em;
          text-transform: uppercase;
          border: none;
          padding: 20px 57px;
          background: #7bb899;
          border-radius: 4px;
          transition: 0.3s all ease;
          cursor: pointer;
          @media (max-width: 1366px) {
            padding: 10px 30px;
          }
          &:hover {
            opacity: 0.6;
          }
        }
      }
    }
  }
}
</style>