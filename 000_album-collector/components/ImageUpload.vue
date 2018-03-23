<template lang="pug">
div.art-preview(v-if="newAlbum.art")
    img(:src='newAlbum.art')
    input(type="file" @change="changeHandler")
</template>
<script>
export default {
  props: ['newAlbum'],
  methods: {
    changeHandler() {
      this.$emit('change', {
        input: this.inputName,
        inputValue: this.inputValue
      });
    }
  }
};
</script>