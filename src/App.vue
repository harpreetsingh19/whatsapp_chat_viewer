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
  font-family: sans-serif,Avenir, Helvetica, Arial;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ff0000;
  margin: 0;
  padding: 0;
  /* background-image: url("./assets/adrien-olichon-ilVYjf0J378-unsplash.jpg");
  background-repeat: repeat-y;
  background-size: auto; */
  
}


</style>
