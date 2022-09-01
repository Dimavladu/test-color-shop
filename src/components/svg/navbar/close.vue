<template>
  <svg
    width="24"
    height="24"
    viewBox="0 0 24 24"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      :class="$attrs.sub_close"
      d="M18 6L6 18"
      stroke="#1F2020"
      stroke-width="1.4"
      stroke-linecap="round"
      stroke-linejoin="round"
    />
    <path
      :class="$attrs.sub_close"
      d="M6 6L18 18"
      stroke="#1F2020"
      stroke-width="1.4"
      stroke-linecap="round"
      stroke-linejoin="round"
    />
  </svg>
</template>

<script>
export default {
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.sub_close {
  padding: 2px;
  cursor: pointer;
  opacity: 0.2;
  transition: 0.3s all ease;
  &:hover {
    opacity: 0.5;
  }
}
</style>