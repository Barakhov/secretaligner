<template>
  <div class="base-dropdown">
    <button
      @click="toggle"
      v-click-outside="hide"
      class="base-button__dropdown base-button d-f jc-sb"
    >
      <span>{{ text }}</span>
      <i class="base-button__icon-right fas fa-chevron-down"></i>
    </button>
    <div class="base-dropdown__options" v-show="isOpen">
      <div
        class="base-dropdown__option"
        v-for="option in optionList"
        :key="option.index"
        @click="set(option)"
      >
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script>
import ClickOutside from "vue-click-outside";

export default {
  username: "BaseDropdown",
  data() {
    return {
      isOpen: false,
      selected: "",
    };
  },
  props: {
    text: {
      type: String,
      default: "",
    },
    optionList: {
      type: Array,
    },
  },
  methods: {
    toggle: function () {
      this.isOpen = !this.isOpen;
    },
    show: function () {
      this.isOpen = true;
    },
    hide: function () {
      this.isOpen = false;
    },
    set: function (option) {
      this.selected = option;
      this.hide();
    },
  },
  directives: {
    ClickOutside,
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/scss/components/_button.scss";

.base-dropdown {
  position: relative;

  &__options {
    position: absolute;
    width: 100%;
    transform: translateY(10px);
    z-index: 1;
    border-radius: 5px;
    box-shadow: 0px 0px 15px -5px;
    background-color: $clr-white;

    ::before {
      content: "";
      display: block;
      position: absolute;
      top: -16px;
      right: 12px;
      width: 20px;
      height: 18px;
      background-color: $clr-white;
      -webkit-clip-path: polygon(50% 45%, 0% 100%, 100% 100%);
      clip-path: polygon(50% 45%, 0% 100%, 100% 100%);
      z-index: -1;
    }
  }

  &__option {
    padding: 10px 15px;
    border-radius: 5px;
    cursor: pointer;
    background-color: $clr-white;
    transition: all 0.15s ease-in-out;

    &:hover {
      background-color: $clr-ultra-light-grey;
    }
  }
}
</style>
