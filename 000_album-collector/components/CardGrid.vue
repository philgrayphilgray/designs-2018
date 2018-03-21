<template lang="pug">
  div
    .card-container
        Card(v-for="(album, index) in $store.state.albums" :album="album" :key="index")
    
</template>

<script>
import Card from '../components/Card';
export default {
  components: {
    Card
  }
};
</script>

<style>
.card-container {
  width: 100%;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.card-container .Card {
  margin: 1em;
}
</style>


