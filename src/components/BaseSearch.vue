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
    border-radius: 5px;
    padding: 15px 15px 15px 60px;
    margin-bottom: 0;
  }
}
</style>
