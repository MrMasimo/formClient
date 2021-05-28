<template>
  <div id="app">
    <FormClient />
  </div>
</template>

<script>
import FormClient from '@/components/FormClient.vue'

export default {
  name: 'App',
  components:{
    FormClient,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
