<template lang="pug">
.userControls
    input.userControls__search(:class="search ? '--active' : null" type="text" role="search" placeholder="search" aria-label="Search field" ref="searchInput")
    button.userControls__button(aria-label="Search button" @click="searchButtonHandler")
        img.userControls__icon(src="~/assets/svg/search.svg" alt="Magnifying glass")
    button.userControls__button(aria-label="Sort by rating")
        img.userControls__icon(src="~/assets/svg/equalizer.svg" alt="Rating sort")
    button.userControls__button(aria-label="Sort by title")
        img.userControls__icon(src="~/assets/svg/equalizer2.svg" alt="Alphabetical sort")
</template>
<script>
export default {
  data() {
    return {
      search: false
    };
  },
  methods: {
    searchButtonHandler() {
      this.search = !this.search;
      this.$refs.searchInput.focus();
    }
  }
};
</script>
<style lang="scss">
.userControls {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-end;

  background: #aaa;
  padding: 1em 0.5em;
}

.userControls__icon {
  height: 2em;
  width: 2em;
}
.userControls__button {
  cursor: pointer;
  background: transparent;
  border: transparent;
}
.userControls__search {
  width: 0;
  padding: 0;
  margin: 0;
  border: none;
  transition: all 0.5s ease-in-out;
}
.userControls__search.--active {
  padding: 0.5em;

  flex: 3 0 50%;
}
</style>
