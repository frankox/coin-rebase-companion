<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App" v-if="false"/>
  <PriceAndRebase crypto="TIME" currency="EUR"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import PriceAndRebase from './components/PriceAndRebase.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    PriceAndRebase
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: aliceblue;
  margin-top: 60px;
}
</style>
