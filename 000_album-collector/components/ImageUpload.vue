<template lang="pug">
div
  label.sr-only(for="fileInput") Upload an album cover
  input#fileInput.sr-only(type="file" ref="fileInput" @change="onFileSelected")
  figure(@click="changeImage")
    div.dragHere(@mouseleave="dontChangeImage" v-if="show" @click="$refs.fileInput.click()")
      div.drag-content(aria-relevant)
        div.icon
          img(src="~/assets/svg/cloud-upload.svg")
        div.outer-bar(v-if="upload")
          div.inner-bar(:style="{width: percentage + '%'}")
        div
          p(v-if="upload")
            strong Nice!
            |
            span(v-if="percentage>25")   Almost there!
          p(v-else) 
            |
            strong Click
            |  to upload an image.
            
    img.image-uploaded(:src="art")
  //- button(@click.prevent="onUpload") Upload
</template>
<script>
import axios from 'axios';
export default {
  data() {
    return {
      art: '',
      upload: null,
      percentage: 0,
      show: true
    };
  },
  methods: {
    onFileSelected: function(e) {
      this.upload = e.target.files[0];
      this.onUpload();
    },
    changeImage() {
      if (this.art) {
        this.show = true;
      }
    },
    dontChangeImage() {
      if (this.art) {
        this.show = false;
      }
    },
    onUpload() {
      const uploadFileFunction = process.env.UPLOAD_FILE_FUNCTION;
      const fd = new FormData();
      fd.append('file', this.upload, this.upload.name);
      axios
        .post(uploadFileFunction, fd, {
          onUploadProgress: uploadEvent => {
            console.log(uploadEvent);
            this.percentage = Math.round(
              uploadEvent.loaded / uploadEvent.total * 100
            );
          }
        })
        .then(res => {
          this.art = res.data.url[0];
          if (this.art) {
            this.changeHandler(this.art);
          }
        });
    },
    changeHandler(uploadUrl) {
      this.$emit('uploaded', { url: uploadUrl });
      this.upload = null;
      this.percentage = 0;
      this.show = false;
    }
  }
};
</script>

<style>
figure {
  position: relative;
  margin: 0 auto;
  height: 300px;
  width: 300px;
  background: #ccc;
  display: flex;
  align-items: center;
  justify-content: center;
}
.image-uploaded {
  max-width: 100%;
  height: auto;
}

.dragHere {
  position: absolute;
  height: 250px;
  width: 250px;
  background: rgba(221, 221, 221, 0.303);
  border: 3px dashed rgb(221, 221, 221);
  display: flex;
  justify-content: center;
  align-items: center;
}

.dragHere:hover {
  background: rgba(221, 221, 221, 0.503);
}
.green-border {
  border: 2px solid green;
}

.outer-bar {
  position: relative;
  margin: 1em 0;
  width: 100%;
  height: 20px;
  border: 1px solid #555;
  background: #fff;
  overflow: hidden;
}
.inner-bar {
  position: absolute;
  background: rgb(46, 140, 88);
  width: 0%;
  height: 20px;
  transition: all 1s ease-in;
}
.drag-content {
  width: 200px;
}
.icon {
  flex-basis: 100%;
}
</style>
