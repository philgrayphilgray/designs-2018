<template lang="pug">
div 
  UserControls
  CardGrid(:albums="$store.state.albums")
</template>


<script>
import UserControls from "../components/UserControls";
import CardGrid from "../components/CardGrid";
export default {
  components: {
    UserControls,
    CardGrid
  }
};
</script>

