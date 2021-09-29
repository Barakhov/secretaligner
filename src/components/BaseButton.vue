<template>
  <button
    @click="$emit('click')"
    class="base-button"
    :class="small ? 'base-button--small' : ''"
  >
    <i
      v-if="icon"
      class="base-button__icon-left fas"
      :class="[{ fa: true }, icon ? 'fa-' + icon : '']"
    ></i>
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
    small: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/scss/components/_button.scss";
</style>
