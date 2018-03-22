<template lang="pug">
div(@keyup.esc="toggleOverlay")
    Overlay(v-if="$store.state.navToggled" :toggle="toggleOverlay")
      div(slot="navigation")
        Navigation
    header
        button.menu-button(@click="toggleOverlay" type="button" aria-label="Toggle navigation" :aria-expanded="$store.state.navToggled")
          span.icon-bar
          span.icon-bar
          span.icon-bar
        .logo
          nuxt-link(to="/")
            img(src="~/assets/svg/logo.svg" alt="Album Collector")

</template>


<script>
import Overlay from '../components/Overlay';
import Navigation from '../components/Navigation';

export default {
  components: { Overlay, Navigation },

  methods: {
    toggleOverlay() {
      this.$store.commit('toggleNav');
    }
  }
};
</script>

<style lang="scss" scoped>
header {
  width: 100%;
  background: #403c3c;
  height: 56px;
  color: #fff;
  display: flex;
  align-items: center;

  justify-content: space-between;
}
.logo {
  margin: auto;
}

.menu-button {
  margin-left: 1em;
  border-color: transparent;
  background-color: transparent;
  background-image: none;

  position: absolute;
  padding: 1em;
  justify-self: start;
  &:hover {
    cursor: pointer;
  }
}

.icon-bar {
  display: block;
  background: #fff;
  height: 3px;
  width: 22px;
  border-radius: 1px;
}

.icon-bar + .icon-bar {
  margin-top: 4px;
}
</style>