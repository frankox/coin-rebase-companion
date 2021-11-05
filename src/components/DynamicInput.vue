<template>
  <label for="rebase-rate-input">REBASE RATE: </label>
  <input v-show="isInputVisible" @auxclick="hideInput"
         @blur="hideInput" @change="onRebaseRateChange"
         class="input-field" id="rebase-rate-input"
         ref="rebase-rate-input" placeholder="%" value="0.599">
  <p  v-show="!isInputVisible" @click="showInput" id="rebase">{{rebaseText}}</p>
</template>

<script>
export default {
  name: "DynamicInput",
  props: {
    defaultRebase: String
  },
  data(){
    return{
      isInputVisible: false,
      rebaseRateInput: this.defaultRebase,
      rebaseText: this.defaultRebase
    }
  },
  methods: {
    showInput() {
      this.isInputVisible = true
    },
    hideInput() {
      this.isInputVisible = false
    },
    onRebaseRateChange() {
      this.rebaseText = this.$refs["rebase-rate-input"].value
      this.rebaseRateInput = this.rebaseText
    }
  }
}
</script>

<style scoped>
input {
  background: transparent;
  color: aliceblue;
  text-align: center;
}
p{
  text-align: center;
  color:aliceblue;
}
</style>