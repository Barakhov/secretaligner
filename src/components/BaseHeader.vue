<template>
  <header class="base-header d-f ai-c jc-fe">
    <div class="base-header__user">
      <span class="base-header__user__icon d-f ai-c jc-c">
        <i class="base-header__user__arrow far fa-user"></i>
      </span>

      <span class="base-header__user__name">{{ username }}</span>
      <i class="base-header__user__arrow fas fa-chevron-down"></i>
    </div>
  </header>
</template>

<script>
export default {
  username: "BaseHeader",
  props: {
    username: String,
  },
};
</script>

<style lang="scss" scoped>
.base-header {
  position: fixed;
  width: 100%;
  height: $header-height;
  background-color: $clr-dark-grey;
  color: $clr-white;
  padding: 0 55px;
  z-index: 2;

  &__user {
    display: flex;
    align-items: center;
    cursor: pointer;

    &__icon {
      border: 2px solid $clr-white;
      border-radius: 100%;
      width: 38px;
      height: 38px;
    }

    &__name {
      font-size: 14px;
      padding: 0 10px;
    }
  }
}
</style>
