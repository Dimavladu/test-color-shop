<template>
  <body :class="{ hidden: overflow }">
    <div>
      <nav-bar
        :cartItems="cartItems"
        :height="height"
        @changeCartItems="(items) => changeCartItems(items)"
        @changeModalVisible="(modalValue) => (overflow = modalValue)"
      />
      <slider :sliderList="sliderList" :sliderWidth="width" />
      <main-content
        :colorItems="colorsList"
        v-model="filterList"
        @addCard="(cardItem) => addCard(cardItem)"
        @selectedValue="(selectedValue) => sortingItems(selectedValue)"
      />
    </div>
  </body>
</template>

<script>
import { ref, onMounted, onBeforeUnmount, watch, computed } from "vue";
import { colorsData, slidersData } from "./service";

import slider from "./components/slider.vue";
import navBar from "./components/navbar.vue";
import mainContent from "./components/mainContent.vue";
export default {
  name: "App",
  components: { navBar, slider, mainContent },

  setup() {
    const colorsList = ref(colorsData);
    const sliderList = ref(slidersData);
    const width = ref();
    const height = ref();
    const cartItems = ref([]);
    const filterList = ref([]);
    const overflow = ref(false);

    watch(
      filterList,
      () => {
        colorsList.value = colorsData;
        filterList.value.map((type) => {
          filteringList(type);
        });
      },
      { deep: true }
    );

    onMounted(() => {
      window.addEventListener("resize", handleResize);
      handleResize();
    });
    onBeforeUnmount(() => {
      window.removeEventListener("resize", handleResize);
    });
    const handleResize = () => {
      width.value = window.innerWidth;
      height.value = window.innerHeight;
    };

    const filteringList = (type) => {
      colorsList.value = colorsList.value.filter((item) =>
        item.type.includes(type)
      );
    };

    const sortingItems = (sortType) => {
      if (sortType === "low_price") {
        colorsList.value.sort((a, b) => a.price - b.price);
      } else if (sortType === "high_price") {
        colorsList.value.sort((a, b) => b.price - a.price);
      } else if (sortType === "new") {
        colorsList.value.sort((a) => (a.type.includes("new") ? -1 : 0));
      } else if (sortType === "popular") {
        colorsList.value.sort((a) => (a.type.includes("sale") ? -1 : 0));
      }
    };

    const addCard = (emitedValue) => {
      if (cartItems.value.includes(emitedValue)) {
        cartItems.value.map((item) => {
          if (item === emitedValue) {
            item.count++;
            return;
          }
        });
      } else {
        emitedValue.count = 1;
        cartItems.value.push(emitedValue);
      }
    };
    const changeCartItems = (items) => {
      cartItems.value = items;
    };

    return {
      colorsList,
      overflow,
      sliderList,
      filterList,
      handleResize,
      width,
      height,
      addCard,
      cartItems,
      sortingItems,
      changeCartItems,
    };
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&display=swap");
body {
  margin: 0;
  font-family: "Inter", sans-serif;
  font-weight: 400;
  overflow-x: hidden;
  width: 100%;
  position: relative;
}
.hidden {
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  height: 100%;
  max-height: 100vh;
  overflow: hidden;
  // padding-bottom: 1px;
}
</style>
