<template>
  <div id="app">
    <Autocomplete :items = "[ 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']" />
  </div>
</template>

<script>
import Autocomplete from './components/Autocomplete'

export default {
  name: 'App',
  components: {
   Autocomplete
  },

  }
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
