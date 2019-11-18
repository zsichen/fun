<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <gen msg="For generate strong password"/>
    
  </div>
</template>

<script>
import gen from './components/gen.vue'

export default {
  name: 'app',
  components: {
    gen
  }
}


</script>




<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #324961;
  margin-top: 60px;
}
</style>
