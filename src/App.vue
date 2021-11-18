<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App" v-if="false"/>
  <PriceAndRebase crypto="TIME" currency="EUR" @price-updated="stakedValue = onPriceUpdated($event)"/>
  <div class="bodyRow">
    <TotalStakedData currencyText="EUR: "/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import PriceAndRebase from './components/PriceAndRebase.vue'
import TotalStakedData from "@/components/TotalStakedData";

export default {
  name: 'App',
  components: {
    HelloWorld,
    PriceAndRebase,
    TotalStakedData,
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
  background-color: black;
}

.bodyRow {
  width:100%;
  margin-top:10px;
  background:transparent;
  border-bottom: 3px solid cadetblue;
  display: flex;
  flex-direction: row;
  align-items: center;
  grid-auto-rows: minmax(50px, auto);
  gap: 50px;
}
</style>
