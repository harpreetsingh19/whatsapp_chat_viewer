<template>
  <div id="app">
    <reader></reader>
  </div>
</template>

<script>
import reader from "@/components/reader.vue"
export default {
  name: 'App',
  components: {reader
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
