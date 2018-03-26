<template lang="pug">
  .card
    img.card__image(:src="album.art" :alt="'Album artwork for ' + album.title + ' by ' + album.artist")
    .card__details
      p {{album.title}}
      p {{album.artist}}
      p {{album.year}}
      span
        Star(v-for="(star, index) in stars" :power="star" :key="index")
    .card__controls
      button.card__button
        img.card__icon(src="~/assets/svg/pencil.svg")
      button.card__button
        img.card__icon(src="~/assets/svg/bin.svg")
    
</template>

<script>
import Star from "./Star";
export default {
  data() {
    return {
      stars: []
    };
  },
  props: ["album"],
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

<style lang="scss">
.card {
  display: flex;
  flex-wrap: wrap;
  width: 310px;
  padding: 1em;
  box-shadow: 1px 4px 2px 1px #aaa;
}

.card__image {
  flex: 100%;
}

.card__details {
  flex: 60%;
  padding: 1em;
}

.card__controls {
  display: flex;
  flex-wrap: wrap;
  width: 2em;
  justify-content: center;
  align-items: center;
}

.card__button {
  padding: 0.25em;
  background: transparent;
  border-color: transparent;
  &:hover {
    cursor: pointer;
  }
}

.card__icon {
  width: 2em;
}
</style>
