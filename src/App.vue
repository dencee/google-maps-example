<template>
  <!-- <locations></locations> -->
  <google-map />
</template>

<script>
import GoogleMap from './components/GoogleMap.vue'
//import Locations from './components/Locations.vue'

export default {
  name: 'App',
  components: {
//    Locations,
    GoogleMap
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
