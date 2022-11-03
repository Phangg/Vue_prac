<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- {{ message }}     -->
    <!-- <HelloWorld my-msg="message"/> -->
    <HelloWorld 
      :my-msg="message"
      @my-event="printMessage"
    />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data: function () {
    return {
      message: "어우 힘들어"
    }
  },
  methods: {
    printMessage: function (obj) {
      console.log(obj.a)
      console.log(obj.b)
      console.log(obj.c)
    }
  },
  components: {
    HelloWorld
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
