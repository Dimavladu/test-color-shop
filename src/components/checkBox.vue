<template>
  <div class="checkbox">
    <div class="checkbox_wrapper" @click="changeToggle">
      <div class="checkbox_body" :class="{ active_bg: toggle }">
        <dot-svg color="black" :class="{ active_dot: toggle }" />
      </div>
    </div>
    <div class="checkbox_text">
      <slot />
    </div>
  </div>
</template>

<script>
import dotSvg from "./svg/dot.vue";
import { ref } from "vue";

export default {
  components: { dotSvg },
  emits: ["changeType"],
  setup(_, { emit }) {
    const toggle = ref(false);
    const changeToggle = () => {
      toggle.value = !toggle.value;
      emit("changeType");
    };
    return { toggle, changeToggle };
  },
};
</script>

<style lang="scss" scoped>
.active_bg {
  transition: 0.3s all ease;
  background: #7bb899;
  border-radius: 40px;
}
.active_dot {
  left: 25%;
  transform: translate(50%, -50%);
}
.checkbox {
  display: flex;
  align-items: center;
  margin-top: 10px;
  gap: 5px;
  &_wrapper {
    transition: 3s all ease;
    width: 36px;
    height: 22px;
    background: #f2f2f2;
    border-radius: 40px;
  }
  &_body {
    cursor: pointer;
    width: 100%;
    height: 100%;
    position: relative;
    transition: 0.3s all ease;
    &:hover {
      opacity: 0.5;
    }
    svg {
      position: absolute;
      top: 50%;
      right: 20%;
      transform: translate(-30%, -50%);
    }
  }
  &_text {
    min-width: 170px;
    font-weight: 400;
    font-size: 12px;
    line-height: 100%;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    color: #1f2020;
  }
}
</style>