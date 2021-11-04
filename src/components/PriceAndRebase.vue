<template>
  <div class="container">
    <div class="priceContainer" id="price-container">
      <p class="subtext">{{crypto}}/{{currency}}</p>
      <h1 id="price" >{{priceText}}</h1>
    </div>
    <div class="rebaseContainer">
      <label for="rebase-rate-input">REBASE RATE: </label><input class="input-field" id="rebase-rate-input" placeholder="%" value = "0.599">
    </div>
  </div>
</template>

<script>
import {coinData} from "@/utils/Apis";
import {cryptos} from "@/utils/Cryptos";


export default{
  name: "PriceAndRebase",
  props : {
    crypto: String,
    currency: String
  },
  data(){
    return{
      priceText: "Loading..."
    }
  },
  methods:{
    updatePrice(){
      setInterval(()=>{
        updatePriceData()
        this.priceText = getPrice()
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

.container {
  width:100%;
  margin-top:10px;
  background:transparent;
  border-bottom: 3px solid #42b983;
  display: grid;
  grid-template-columns: 40% auto 40%;
  align-items: center;
  grid-auto-rows: minmax(50px, auto);
  gap: 50px;
}

.priceContainer{
  margin-left: 20%;
  background:#353535;
  padding: 0 10px;
  text-align:center;
  grid-column: 1;
  grid-row: 1;
}

.rebaseContainer{
  grid-column: 2/3;
  grid-row: 1;
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

input {
  background: transparent;
  color: aliceblue;
  text-align: center;
}

</style>