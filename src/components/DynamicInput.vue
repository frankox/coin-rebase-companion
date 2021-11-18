<template id = "{{id}}">
  <p class="subtext">{{title}}</p>
  <input v-show="isInputVisible" @auxclick="hideInput"
         @blur="hideInput" @change="onRebaseRateChange"
         class="input-field" id="di-input-part"
         ref="dynamic-input-input" placeholder="%">
  <p  v-show="!isInputVisible" @click="showInput"
      id="di-tex-part" @change="$emit('dio', DITextPart)">
    {{ DITextPart }}
  </p>
</template>

<script>
export default {
  name: "DynamicInput",
  emits: ['dio'],
  props: {
    defaultValue: String,
    title: String,
    id: String
  },
  data(){
    return{
      isInputVisible: false,
      rebaseRateInput: this.defaultValue,
      DITextPart: this.defaultValue
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
      this.DITextPart = this.$refs["dynamic-input-input"].value
      this.rebaseRateInput = this.DITextPart
    }
  }
}
</script>

<style scoped>
input {
  background: transparent;
  color: aliceblue;
  text-align: center;
  font-size:1.5em;
  margin-bottom: 7px;
}

.subtext {
  font-size:1em;
  text-transform:uppercase;
  margin-bottom: 10px;
}

p{
  text-align: center;
  color:aliceblue;
  font-size:1.5em;
}
</style>