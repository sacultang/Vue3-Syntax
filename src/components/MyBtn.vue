<template>
  <div>
    <div 
      :class="{large}"
      class="btn"
      :style="{backgroundColor:color}"
    >
      <slot name="icon"></slot>
      <slot name="text"></slot>
     
    </div>
    <input type="text" v-model="msg">
  </div>
</template>

<script>
  export default {
    inheritAttrs:false,
    emits:[
      'heropy',
      'changeMsg'
    ],
    created() {
      console.log(this.$attrs)
    },
    props:{
      color:{
        type:String,
        default:'gray'
      },
      large: {
        type:Boolean,
        default:false
      }
    },
    data(){
      return {
        msg:''
      }
    },
    watch: {
      msg(){
        this.$emit('changeMsg',this.msg)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .btn {
    display: inline-block;
    margin: 4px;
    padding: 6px 12px;
    border-radius: 4px;
    background-color: gray;
    color: white;
    cursor: pointer;
    &.large {
      font-size: 20px;
      padding: 10px 20px;
    }
  }
  
</style>