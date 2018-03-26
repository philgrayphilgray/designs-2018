<template lang="pug">
form.newForm(@submit.prevent="submitHandler")
  ImageUpload(:art="art" @uploaded="imageUploaded")
  FormInput(v-for="(inputElement, index) in Object.keys(newAlbum)" :inputName="inputElement" :key="inputElement" @change="inputHandler")
  button.newForm__submit(type="submit" role="button" aria-labelledby="Submit a new album") Save
</template>


<script>
import FormInput from "../../components/FormInput";
import ImageUpload from "../../components/ImageUpload";
export default {
  components: {
    FormInput,
    ImageUpload
  },
  data() {
    return {
      art: "",
      newAlbum: {
        title: "",
        artist: "",
        year: "",
        rating: ""
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
      this.$store.commit("add", newAlbumWithArt);
      e.target.reset();
      this.$router.push({ path: "/" });
    }
  }
};
</script>
<style>
.newForm {
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
}

.newForm__submit {
  width: 100%;
  padding: 1em 0.25em;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}
</style>
