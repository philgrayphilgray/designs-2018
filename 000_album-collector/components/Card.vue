<template lang="pug">
  .Card
    img(:src="album.art")
    .card-details
      p {{album.title}}
      p {{album.artist}}
      p {{album.year}}
      span
        Star(v-for="(star, index) in stars" :power="star" :key="index")
    .card-controls
    //- controls, edit, delete icons
    
</template>

<script>
import Star from './Star';
export default {
  data() {
    return {
      stars: []
    };
  },
  props: ['album'],
  components: {
    Star
  },
  beforeMount() {
    this.setStars();
  },
  methods: {
    setStars() {
      for (let i = 1; i <= 5; i++) {
        if (i <= this.album.rating) {
          this.stars.push(true);
        } else {
          this.stars.push(false);
        }
      }
    }
  }
};
</script>

<style>
.Card {
  width: 310px;
  padding: 1em;
  box-shadow: 1px 4px 2px 1px #aaa;
}

.Card img {
  max-width: 100%;
}
</style>
