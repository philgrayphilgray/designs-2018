<template lang="pug">
  .overlay(@click="toggle" role="dialog")
      button.menu-button-close(role="button" alt="Close menu" aria-label="Toggle navigation off" :aria-expanded="$store.state.navToggled")
        span.sr-only Toggle navigation
        span.icon-bar
        span.icon-bar
        span.icon-bar
      .overlay-content
        slot(name="navigation")
</template>
<script>
export default {
  props: ['toggle']
};
</script>
<style lang="scss" scoped>
.overlay {
  height: 100vh;
  width: 100vw;
  background: #000;
  color: #fff;
  position: fixed;
  overflow: auto;

  z-index: 100;
}
.overlay-content {
  height: 100vh;
  display: flex;
  justify-content: center;
}
.overlay-content > * {
  padding-top: 10em;
}
.menu-button-close {
  margin: 1em;
  border-color: transparent;
  background-color: transparent;
  background-image: none;
  right: 0;
  position: absolute;
  padding: 1em;

  transform: translate3d(0, 0, 0);
  z-index: 10;
  transition: all 0.1s ease-out;

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
  transform-origin: 21px;
}
.icon-bar:nth-child(3) {
  opacity: 0;
}
.icon-bar:nth-child(2) {
  transform: rotate(-45deg);
}
.icon-bar:nth-child(4) {
  transform: rotate(45deg);
}
.icon-bar + .icon-bar {
  margin-top: 4px;
}
</style>
