<template>
  <div class="row">
    <div class="rowItem1">
      <DynamicInput id="staked" title="STAKED:" default-value="1" />
    </div>
    <div class="rowItem2">
      <h3 id="total-staked-value-title">EUR: </h3>
      <span id="total-staked-value">{{stakedValue}}</span>
    </div>
  </div>
</template>

<script>
import DynamicInput from "@/components/DynamicInput";

export default {
  name: "TotalStakedData",
  components: {DynamicInput},
  data(){
    return{
      stakedValuePlaceholder: 'Loading...',
    }
  },
  computed:{
    stakedValue: ()=>{
      this.$root.on('price_updated', (unitaryPrice)=>{
        this.getStakedValue(unitaryPrice)
      })
    }
  },
methods:{
  setStakedValue(value){
    this.stakedValue = value
  },
  getStakedValue(value){
    const result =  Number(this.stakedValue) * Number(value)
    return result && result > 0? result: 'Loading...'
  },
  mounted(){
    this.$root.on('price_updated', (unitaryPrice)=>{
      this.setStakedValue(this.getStakedValue(unitaryPrice))
      console.log("PUTANA")
    })
    this.$root.on('staked_dynamic_input_value_changed', (unitaryPrice)=>{
      this.setStakedValue(this.getStakedValue(unitaryPrice))
      console.log("PUTANA")
    })
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