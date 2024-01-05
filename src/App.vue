<template>
  <!--<img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>-->

  <LeafletMap />
</template>

<script>
import LeafletMap from './components/LeafletMap.vue'

export default {
  name: 'App',
  components: {
    LeafletMap
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
#app {
  height: 100%;
  width: 100%;
}
</style>
