<template lang="pug">
div.new-form
  strong.line-through Album Details
  ImageUpload(:art="art" @uploaded="imageUploaded")
  form(@submit.prevent="submitHandler")
    FormInput(v-for="(inputElement, index) in Object.keys(newAlbum)"  :inputName="inputElement" :key="inputElement" @change="inputHandler")
    button.button-submit(type="submit" role="button" aria-labelledby="Submit a new album") save
</template>


<script>
import FormInput from '../../components/FormInput';
import ImageUpload from '../../components/ImageUpload';
export default {
  components: {
    FormInput,
    ImageUpload
  },
  data() {
    return {
      art: '',
      newAlbum: {
        title: '',
        artist: '',
        year: '',
        rating: ''
      }
    };
  },

  methods: {
    imageUploaded: function({ url }) {
      this.art = url;
    },
    inputHandler: function({ input, inputValue }) {
      this.newAlbum[input] = inputValue;
    },
    submitHandler(e) {
      const newAlbumWithArt = { ...this.newAlbum, art: this.art };
      this.$store.commit('add', newAlbumWithArt);
      e.target.reset();
      this.$router.push({ path: '/' });
    }
  }
};
</script>
<style>
.new-form {
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
}

.art-preview {
  margin: 0 auto;
}
.line-through {
  display: block;
  position: relative;
  text-align: center;
  width: 100%;
  z-index: 1;
  background: #fff;
  padding: 0.5em;
}

.line-through:before {
  background-color: #fff;
  content: '';
  position: absolute;
  top: 50%;
  z-index: -1;
}

.line-through:after {
  border-bottom: 1px solid #dfe0e6;
  content: '';
  display: block;
  position: absolute;
  top: 49%;
  width: 100%;
  z-index: -2;
}

.button-submit {
  width: 100%;
  padding: 1em 0.25em;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}
</style>
