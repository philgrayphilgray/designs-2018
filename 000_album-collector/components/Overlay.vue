<template lang="pug">
  .overlay(@click="toggle" role="dialog")
    img.menu-button-close(src="~/assets/svg/cross.svg")
    .overlay-content
      slot(name="navigation")
</template>
<script>
export default {
  props: ['toggle']
  // TODO: tabtrapping
};
</script>
<style lang="scss">
.overlay {
  height: 100vh;
  width: 100vw;
  background: #000;
  color: #fff;
  position: absolute;

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
  background: white;
  position: absolute;
  right: 0;
  margin: 1em;
  padding: 1em;
  justify-self: start;
  &:hover {
    cursor: pointer;
  }
}
</style>
