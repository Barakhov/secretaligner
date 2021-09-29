<template>
  <div class="base-title">
    <i class="far fa-address-card base-title__icon"></i>
    <div class="base-title__text">
      <h1 class="base-title__text__main">
        <slot></slot>
      </h1>
      <p class="base-title__text__secondary">
        <slot name="secondary"></slot>
      </p>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped lang="scss">
.base-title {
  width: 100%;
  display: flex;
  align-items: center;
  margin: 20px 0;

  &__icon {
    font-size: 20px;
    margin-right: 15px;
  }

  &__text {
    &__main {
      font-size: 24px;
      color: $clr-dark-grey;
    }

    &__secondary {
      color: $clr-mid-grey;
    }
  }
}
</style>
