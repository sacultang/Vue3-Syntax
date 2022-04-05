<template>
  <div>
    <!-- <h1>{{msg}}</h1>
    <input type="text"
      v-model="msg"
    >
    <h1>{{checked}}</h1>
    <input type="checkbox" v-model="checked"> -->
    <!-- <MyBtn class="heropy" @heropy="log" @changeMsg="logMsg">
      <template #text>
        <span style="color:red;">Banana</span>
      </template>
      <template #icon>
        <span style="color:red;">(B)</span>
      </template>
      
    </MyBtn> -->

    
    <!-- <template v-if="isShow">
      <h1>Title</h1>
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
    </template> -->
    <!-- <h1 ref="hello">
      Hello world!
    </h1> -->
    <Hello ref="hello"></Hello>
  </div>
</template>

<script>
  // import Fruits from './components/Fruits'
  import Hello from '~/components/Hello'
  import MyBtn from '~/components/MyBtn.vue'
  import Parent from '~/components/Parent'
  import { computed } from 'vue'
  import shortid from 'shortid'
  export default {
    
    components :{
      // Fruits
      MyBtn,
      Parent,
      Hello
      // Child
    },
    created(){
      console.log(this.$refs.hello)
    },
    mounted (){
      const h1El = this.$refs.hello
      console.log(h1El.$refs.good)
    },
    data(){
      return {
        // Getter, Setter
        // msg: 'Hello world',
        isActive: false,
        fontStyle:{
          color:'orange',
          fontSize:'30px' 
        },
        backgroundStyle:{
          backgroundColor:'black'
        },
        isShow:false,
        count:0,
        fruits:['Apple','Banan','Cherry'],
        checked:false,
        color:'#000',
        message:'Hello World'
      }
    },
    provide(){
      return {
        msg: computed(() => {
          return this.message
        })
      }
    }
    ,
    computed: {
      // Getter
      // revesedMessage(){
      //   return this.msg.split('').reverse().join('')
      // }
      revesedMessage () {
        return this.msg.split('').reverse().join('')
      },
      newFruits(){
        return this.fruits.map(fruit => ({
          id:shortid.generate(),
          name:fruit
        }))
      }
    },
    watch:{
      // msg(newValue){
      //   console.log('msg watch: ',newValue)
      // },
      // revesedMessage(){
      //   console.log(this.revesedMessage)
      // }
      msg(){
        console.log(this.msg.trim())
      }
    },
    methods: {
      add(){
        this.msg = 'Good!'
      },
      activate() {
        this.isActive = !this.isActive
      },
      changeStyle(){
        this.fontStyle.color='red'
        this.fontStyle.fontSize ='50px'
      },
      handler(){
          // this.isShow = !this.isShow
          // this.count += 1
          console.log('msg,e')
      },
      handlerA(){
        console.log('Enter!!')
        
      },
      handlerB(){
        console.log('child')
      },
      log(e){
        console.log('click')
        console.log(e)
      },
      logMsg(msg){
        console.log(msg)
      }
    }
    
  }
</script>

<style lang="scss" scoped>
  .active {
    color: red;
    font-weight: bold;
  }
  .color {
    width: 300px;
    height: 300px;
  }
  .parent {
    width: 200px;
    height: 100px;
    background-color: royalblue;
    padding: 10px;
    overflow: auto;
    .child {
      width: 100px;
      height: 2000px;
      background-color: orange;
    }
  }
</style>