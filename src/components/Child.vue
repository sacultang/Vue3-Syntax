<template>
  <div>
    child : {{msg.value}}
  </div>
</template>

<script>
  export default {
    inject:[
      'msg'
    ]
  }
</script>

<style lang="scss" scoped>

</style>