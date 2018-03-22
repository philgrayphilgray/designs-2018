<template lang="pug">
  div.new-form
    h1 Add New Album
    div.art-preview(v-if="newAlbum.art")
      img(:src='newAlbum.art')
    form(@submit.prevent="submitHandler")
      strong.line-through Album Details
      FormInput(v-for="(inputElement, index) in Object.keys(newAlbum)"  :inputName="inputElement" :key="inputElement" @change="inputHandler")
      button.button-submit(type="submit" role="button" aria-labelledby="Submit a new album") save
</template>


<script>
import FormInput from '../../components/FormInput';
export default {
  components: {
    FormInput
  },
  data() {
    return {
      newAlbum: {
        title: '',
        artist: '',
        art: 'http://via.placeholder.com/300x300', // use prop validation to set default?
        year: '',
        rating: ''
      }
    };
  },
  methods: {
    inputHandler: function({ input, inputValue }) {
      this.newAlbum[input] = inputValue;
    },
    submitHandler(e) {
      this.$store.commit('add', this.newAlbum);
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
