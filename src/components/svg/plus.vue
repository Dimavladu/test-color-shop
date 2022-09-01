<template>
  <svg
    :class="$attrs.plus"
    width="20"
    height="20"
    viewBox="0 0 20 20"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      id="path"
      d="M10 4.16663V15.8333"
      :stroke="stroke"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    />
    <path
      id="path"
      d="M4.16699 10H15.8337"
      :stroke="stroke"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    />
  </svg>
</template>

<script>
export default {
  props: {
    stroke: {
      type: String,
      required: false,
    },
  },
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
// .plus > * {
//   stroke: #000;
// }
</style>