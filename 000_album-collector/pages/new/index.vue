<template lang="pug">
  div.new-form
    img(:src="art")
    form(@submit.prevent="submitHandler")
      strong.line-through Album Details
      //- ImageUpload(:newAlbum="newAlbum" @change="")
      input(type="file" @change="onFileSelected")
      button(@click.prevent="onUpload") Upload
      FormInput(v-for="(inputElement, index) in Object.keys(newAlbum)"  :inputName="inputElement" :key="inputElement" @change="inputHandler")
      button.button-submit(type="submit" role="button" aria-labelledby="Submit a new album") save
</template>


<script>
import axios from 'axios';

import FormInput from '../../components/FormInput';
import ImageUpload from '../../components/ImageUpload';
export default {
  components: {
    FormInput,
    ImageUpload
  },
  data() {
    return {
      upload: null,
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
    onFileSelected: function(e) {
      this.upload = e.target.files[0];
    },
    onUpload() {
      const uploadFileFunction = process.env.UPLOAD_FILE_FUNCTION;
      const fd = new FormData();
      fd.append('file', this.upload, this.upload.name);
      axios
        .post(uploadFileFunction, fd, {
          onUploadProgress: uploadEvent => {
            console.log(uploadEvent);
            console.log(
              'Upload Progress: ' +
                Math.round(uploadEvent.loaded / uploadEvent.total * 100) +
                '%'
            );
          }
        })
        .then(res => {
          this.art = res.data.url[0];
          console.log(res);
        });
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
