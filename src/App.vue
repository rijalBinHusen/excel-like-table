<template>
  <excel-table></excel-table>
</template>

<script>
import ExcelTable from "./components/ExcelTable.vue"

export default {
  name: 'App',
  components: {
    ExcelTable
  }
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
