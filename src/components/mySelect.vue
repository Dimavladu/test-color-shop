<template>
  <div class="select">
    <div class="select_wrapper">
      <div class="selected" v-if="!optionsToggle" @click="optionsToggle = true">
        {{ selected.name }}
        <options-arrow class="selected_arrow" />
      </div>
      <div class="options" v-else-if="optionsToggle">
        <div class="options_wrapper" @click="optionsToggle = false"></div>
        <div
          class="option"
          v-for="option in options"
          :key="option.value"
          @click="selectOption(option)"
        >
          {{ option.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import optionsArrow from "./svg/optionsArrow.vue";

export default {
  emits: ["selectedValue"],
  components: { optionsArrow },
  setup(_, { emit }) {
    const options = ref([
      { name: "Сначала недорогие", value: "low_price" },
      { name: "Сначала дорогие", value: "high_price" },
      { name: "Сначала популярные", value: "popular" },
      { name: "Сначала новые", value: "new" },
    ]);
    const selected = ref();
    const optionsToggle = ref(false);
    const selectOption = (option) => {
      selected.value = option;
      optionsToggle.value = false;
      emit("selectedValue", selected.value.value);
    };
    selectOption(options.value[0]);
    return { options, selected, optionsToggle, selectOption };
  },
};
</script>

<style lang="scss" scoped>
.select {
  margin-right: 60px;
  &_wrapper {
    position: absolute;
    .selected {
      width: 200px;
      position: relative;
      top: 0;
      left: 0;
      transform: translate(-50%, -50%);
      cursor: pointer;
      display: flex;
      align-items: center;
      transition: 0.3s all ease;
      &_arrow {
        padding: 5px;
      }
      &:hover {
        opacity: 0.5;
      }
    }
    .options {
      position: relative;
      top: 0;
      left: -200px;
      width: 280px;
      &_wrapper {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
        z-index: 4;
      }
      .option {
        position: relative;
        background: #fff;
        z-index: 5;
        padding: 17px 24px;
        cursor: pointer;
        transition: 0.3s all ease;
        &:hover {
          background: #7bb899;
        }
      }
    }
  }
}
</style>