<template lang="pug">
nav(role="navigation")
    ul
        li
            nuxt-link(tag="a" to="/") Home
        li
            nuxt-link(tag="a" to="/new") Add
</template>
<style scoped>
nav {
  text-align: center;
  font-size: 2em;
}
ul {
  list-style: none;
}

li a {
  color: #fff;
  text-decoration: none;
}
</style>
