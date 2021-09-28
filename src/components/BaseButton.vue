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

  i {
    margin-right: 15px;
  }
}
</style>
