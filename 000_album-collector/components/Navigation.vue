<template lang="pug">
.navigation
  .branding
    img(src="~/assets/svg/logo-menu.svg")   
  nav(role="navigation")
      ul
          li
              nuxt-link(tag="a" to="/") Home
          li
              nuxt-link(tag="a" to="/new") Add
</template>
<style scoped>
.navigation {
  justify-self: flex-start;
}
nav {
  text-align: center;
  font-size: 2em;
}
ul {
  list-style: none;
  padding: 0;
}

li a {
  color: #fff;
  text-decoration: none;
}
</style>
