<template>
  <div id="app" class="container-fluid mt-3">
    <div class="jumbotron">
      <h2>NT2: Trabajo Práctico 4</h2>
      <br>
      <Navbar />
      <router-view></router-view>
      <!-- <Formulario />
      <Estructura /> -->
      
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'

export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
#app {
}

h1 {
  color: blue;
}

.jumbotron {
  padding: 32px !important;
}
</style>
