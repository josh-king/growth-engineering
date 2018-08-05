<template>
  <div id="app">
    <div class="container is-fluid">
      <Navigation/>
      <Youtube/>
    </div>
  </div>
</template>

<script>
import Youtube from './components/Youtube.vue'
import Navigation from './components/Navigation.vue'

export default {
  name: 'app',
  components: {
    Youtube,
    Navigation
  }
}
</script>

<style>
</style>
