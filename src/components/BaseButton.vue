<template>
  <button class="base-button">
    <i class="fas" :class="[{ fa: true }, icon ? 'fa-' + icon : '']"></i>
    <span>{{ text }}</span>
  </button>
</template>

<script>
export default {
  username: "BaseButton",
  props: {
    text: {
      type: String,
      default: "",
    },
    icon: {
      type: String,
      default: "",
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/scss/components/_button.scss";
</style>
