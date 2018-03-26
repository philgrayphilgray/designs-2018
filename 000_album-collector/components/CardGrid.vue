<template lang="pug">
.cardGrid
  Card(v-for="(album, index) in $store.state.albums" :album="album" :key="index")
    
</template>

<script>
import Card from "../components/Card";
export default {
  components: {
    Card
  }
};
</script>

<style>
.cardGrid {
  width: 100%;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.cardGrid .card {
  margin: 0.5em;
}
</style>


