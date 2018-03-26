<template lang="pug">
img.starIcon.--star-full(src="~/assets/svg/star-full.svg", alt="Full Star" v-if="power")
img.starIcon.--star-empty(src="~/assets/svg/star-empty.svg", alt="Empty Star" v-else)
</template>

<script>
export default {
  props: ["power"]
};
</script>
