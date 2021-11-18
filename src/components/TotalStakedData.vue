<template>
  <div class="row">
    <div class="rowItem1">
      <DynamicInput id="staked" title="STAKED:" default-value="1" @dio="stakedValue = onStakedAmountUpdated($event)"/>
    </div>
    <div class="rowItem2">
      <h3 id="total-staked-value-title">{{ currencyText }}</h3>
      <span id="total-staked-value" >{{stakedValue}}</span>
    </div>
  </div>
</template>

<script>
import DynamicInput from "@/components/DynamicInput";

export default {
  name: "TotalStakedData",
  components: {DynamicInput},
  props:{
    currencyText: String
  },
  data(){
    return{
      stakedValue: 'Loading...',
      stakedAmount : '1',
      price: '1'
    }
  },
  methods:{
    onStakedAmountUpdated(stakedAmount){
      this.stakedAmount = stakedAmount
      return this.calculateStakedValue(Number(stakedAmount), Number(this.price))
    },
    onPriceUpdated(price){
      console.log(price)
      this.price = price
      return this.calculateStakedValue(Number(this.stakedAmount), Number(price))
    },
    calculateStakedValue(amount, value){
      const result =  amount * value
      return result && result > 0? result: 'Loading...'
    }
  }
}
</script>

<style scoped>
.row {
  width:100%;
  margin-top:10px;
  background:transparent;
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 10px;
}

.rowItem1{
  flex:1
}

.rowItem2{
  flex:2
}
</style>