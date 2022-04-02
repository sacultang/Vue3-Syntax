<template>
  <section v-if="hasFruit">
    <h1>Fruits</h1>
    <ul>
      <li v-for="fruit in fruits" :key="fruit">
        {{fruit}}
      </li>
    </ul>
    <h1>Reverse Fruits</h1>
    <ul>
      <li v-for="fruit in reverseFruits" :key="fruit">
        {{fruit}}
      </li>
    </ul>
  </section>
</template>
<script>
export default {
  data(){
    return {
      fruits : [ 
        'Apple','Banan','Cherry'
      ]
    }
  },
  computed:{
    hasFruit(){
      return this.fruits.length > 0
    },
    reverseFruits(){
      return this.fruits.map(fruit => {
        // split() 'Apple' => ['A','p','p','l','e']
        // reverse() => ['e','l','p','p','A']
        // join() => 'elppA'
        return fruit.split('').reverse().join('')
      })
    }
  }
}
</script>
<style>
  
</style>