<template>
  <div id="app">
   <poke></poke>
  </div>
</template>

<script>
import pokedatos from './components/Pokeguia.vue'
  export default {
    data() {
      return {
        message: 'Hola en vue',
      };
    },
    components: {
      'poke': pokedatos,
    }
  }
</script>

<style scoped>

</style>
