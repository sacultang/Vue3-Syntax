<template>
  <div>
    <h1 
      :class="{ active : isActive }"
      @click="activate()">Hello?!({{ isActive }})</h1>
  </div>
</template>

<script>
  // import Fruits from './components/Fruits'
  export default {
    components :{
      // Fruits
    },
    data(){
      return {
        // Getter, Setter
        msg: 'Hello Computed',
        isActive: false
      }
    },
    computed: {
      // Getter
      // revesedMessage(){
      //   return this.msg.split('').reverse().join('')
      // }
      revesedMessage () {
        return this.msg.split('').reverse().join('')
      }
    },
    watch:{
      msg(newValue){
        console.log('msg watch: ',newValue)
      },
      revesedMessage(){
        console.log(this.revesedMessage)
      }
    },
    methods: {
      add(){
        this.msg = 'Good!'
      },
      activate() {
        this.isActive = !this.isActive
      }
    }
    
  }
</script>

<style lang="scss" scoped>
  .active {
    color: red;
    font-weight: bold;
  }
</style>