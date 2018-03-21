<template lang="pug">
  div 
    h1 Add New Album
    form(@submit.prevent="submitHandler")
      strong.line-through Album Details
      FormInput(v-for="key in Object.keys(newAlbum)" :inputName="key" :key="key")
      button(type="submit") save
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
        art: '',
        year: '',
        rating: ''
      }
    };
  },
  methods: {
    submitHandler(e) {
      this.$store.commit('add', this.newAlbum);
      e.target.reset();
      this.$router.push({ path: '/' });
    }
  }
};
</script>
<style>
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
</style>
