<template>
  <div class="search">
    <i class="search__icon fas fa-search"></i>
    <input
      v-model="searchString"
      @keyup="inputKeyup()"
      class="search__input"
      placeholder="Buscar"
      type="text"
    />
  </div>
</template>

<script>
export default {
  username: "BaseSearch",
  data() {
    return {
      searchString: "",
    };
  },
  methods: {
    inputKeyup() {
      if (this.searchString.length > 2) {
        this.$emit("dosearch", this.searchString);
      } else {
        this.$emit("dosearch", "");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.search {
  position: relative;
  width: 100%;

  &__icon {
    position: absolute;
    top: 50%;
    left: 30px;
    font-size: 18px;
    transform: translateY(-50%);
    color: $clr-dark-grey;
  }

  &__input {
    width: 100%;
    max-width: 530px;
    background-color: $clr-light-grey;
    border-radius: 7px;
    padding: 15px 15px 15px 60px;
    border: none;

    &:focus-visible {
      outline: none;
      box-shadow: 0px 0px 4px -2px $clr-dark-grey;
      background-color: $clr-light-grey;
    }
  }
}
</style>
