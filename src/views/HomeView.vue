<template>
  <div class="home">
    <HelloWorld msg="Bienvenido a la Aplicación de Tareas con Vue.js!"/>
    <img alt="Vue logo" src="../assets/logo.png">
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
