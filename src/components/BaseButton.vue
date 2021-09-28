<template>
  <button class="base-button">
    <img src="@/assets/icons/plus.svg" />

    <!-- <svg viewBox="0 0 32 32">
      <use
        v-bind="{
          'xlink:href': '@/assets/icons/sprite.svg#work',
        }"
      ></use>
    </svg> -->

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
  },
};
</script>

<style lang="scss" scoped>
.base-button {
  cursor: pointer;
  background-color: $clr-white;
  border: 2px solid $clr-primary;
  border-radius: 5px;
  padding: 15px;

  display: flex;
  align-items: center;
  justify-content: center;
  color: $clr-primary;
  font-weight: bold;

  transition: all 0.25s ease-in-out;

  &:hover {
    background-color: $clr-primary;
    color: $clr-white;
  }

  img {
    margin-right: 15px;
    max-width: 15px;
    max-height: 15px;
    display: inline-block;
  }
}
</style>
