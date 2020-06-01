<template>
  <div id="app">
    <PrinterTest></PrinterTest>
  </div>
</template>

<script>
import PrinterTest from './components/PrinterTest.vue'

export default {
  name: 'App',
  components: {
    PrinterTest
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
