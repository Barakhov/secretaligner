<template>
  <div class="base-modal__backdrop">
    <div class="base-modal">
      <button type="button" class="base-modal__close" @click="close">
        <i class="fas fa-times"></i>
      </button>
      <section class="base-modal__body">
        <slot></slot>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: "BaseModal",
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style lang="scss" scoped>
.base-modal {
  min-width: 25%;
  position: relative;
  display: flex;
  flex-direction: column;
  overflow-x: auto;
  padding-top: 40px;
  border-radius: 5px;
  background-color: $clr-white;
  box-shadow: 0px 2px 20px -5px $clr-dark-grey;

  &__backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 2;
  }

  &__body {
    position: relative;
    padding: 0 10px 10px 10px;
  }

  &__close {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    font-size: 20px;
    cursor: pointer;
    color: $clr-primary;
    background-color: transparent;
    height: 40px;
    width: 40px;
  }
}
</style>
