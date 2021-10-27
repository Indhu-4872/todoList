<template>
  <div id="app">
    <NavBar />
    <router-view />
  </div>
</template>

<script>
import NavBar from '../src/components/NavBar.vue'

export default {
  name: 'App',
  components: {
    NavBar
  }
}
</script>
<style lang="scss">
#app {
  font-family:  sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  color: black;
}

</style>
