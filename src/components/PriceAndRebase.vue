<template>
  <div class="header">
    <div class="priceContainer" id="price-container">
      <p class="subtext">{{crypto}}/{{currency}}</p>
      <h1 id="price" >{{priceText}}</h1>
    </div>
    <div class="rebaseContainer">
      <DynamicInput id="rebaseInput" title="REBASE RATE:" default-value="0.599"/>
    </div>
  </div>

</template>

<script>
import {coinData} from "@/utils/Apis";
import {cryptos} from "@/utils/Cryptos";
import DynamicInput from "@/components/DynamicInput";

export default{
  name: "PriceAndRebase",
  components: {
    DynamicInput
  },
  props : {
    crypto: String,
    currency: String
  },
  data(){
    return{
      priceText: 'Loading...',
    }
  },
  methods:{
    updatePrice(){
      setInterval(()=>{
        updatePriceData()
        const price = getPrice()
        if(this.priceText !== price){
          this.priceText = price
          this.$emit('priceUpdated', price)
          console.log('emit')
        }
      }, 3000)
    }
  },
  mounted() {
    selectedParams.crypto = this.crypto
    selectedParams.currency = this.currency
    this.updatePrice()
  },
  updated() {
    selectedParams.crypto = this.crypto
    selectedParams.currency = this.currency
  }
}

const selectedParams = {
  crypto: "Loading...",
  currency: "Loading..."
}

const currentCoinData = {
  wonderland : {
    eur: String,
    usd: String
  },
  olympus : {
    eur: String,
    usd: String
  },
  "klima-dao" : {
    eur: String,
    usd: String
  },
}

//endregion
//region scheduler
function updatePriceData() {
  coinData().then((response)=>{
    currentCoinData.wonderland = response.data.wonderland
    currentCoinData.olympus = response.data.olympus
    currentCoinData["klima-dao"] = response.data["klima-dao"]
  })
}

function getPrice() {
  const cryptoRequest = cryptos[selectedParams.crypto]

  if(cryptoRequest) {
    switch (selectedParams.currency.toUpperCase()) {
      case "EUR" :
        return currentCoinData[cryptoRequest].eur
      case "USD" :
        return currentCoinData[cryptoRequest].usd
    }
  }
  return 'Loading...'
}
//endregion

</script>

<style scoped>

.header {
  width:100%;
  background:transparent;
  border-bottom: 3px solid #42b983;
  display: flex;
  flex-direction: row;
}

.priceContainer{
  background:#353535;
  padding: 0 10px;
  text-align:center;
  flex:1;
  margin-bottom: 10px;
}

.rebaseContainer{
  flex:2
}

.subtext {
  font-size:1em;
  text-transform:uppercase;
  margin-bottom: 10px;
}

h1 {
  margin: 0 0 10px 0;
  align-self: center;
}

p{
  text-align: center;
  color:aliceblue;
}
</style>