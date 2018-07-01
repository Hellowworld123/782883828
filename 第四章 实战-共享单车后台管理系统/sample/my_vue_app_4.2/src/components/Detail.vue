<template>
  <div>
    <h1>这是详情页面</h1>
    {{$route.params.id}}
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
