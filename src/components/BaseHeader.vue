<template>
  <header class="base-header">
    <div class="base-header__user">
      <span class="base-header__user__icon">
        <img src="@/assets/icons/user.svg" alt="user icon" />
      </span>
      <span class="base-header__user__name">{{ username }}</span>
      <span class="base-header__user__arrow">
        <img src="@/assets/icons/arrow-down.svg" alt="arrow down icon" />
      </span>
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
  width: 100%;
  height: $header-height;
  background-color: $clr-dark-grey;
  color: $clr-white;
  padding: 0 55px;
  display: flex;
  align-items: center;
  justify-content: flex-end;

  &__user {
    display: flex;
    align-items: center;
    cursor: pointer;

    &__icon {
      border: 1px solid $clr-white;
      border-radius: 100%;
      padding: 10px;
    }

    &__name {
      font-size: 14px;
      padding: 0 10px;
    }

    img {
      width: 12px;
      height: 12px;
    }
  }
}
</style>
