<template lang="pug">
img(src="~/assets/svg/star-full.svg", alt="Full Star" v-if="power")
img(src="~/assets/svg/star-empty.svg", alt="Empty Star" v-else)
</template>

<script>
export default {
  props: ['power']
};
</script>
