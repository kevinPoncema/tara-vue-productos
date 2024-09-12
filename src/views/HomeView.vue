<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h2>Esta pagina y about son solo rutas de ejemplo revisar Productos</h2>
    <h4>No pidio otras rutas o diseño en especifico </h4>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>
