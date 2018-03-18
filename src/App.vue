<template>
  <div id="app">
    <img src="./assets/wot-logo.svg" width="130px">
    <img src="./assets/logo.png">
    <Home/>
  </div>
</template>

<script>
import Home from './components/Home'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
body {
  background: #f1f1f1;
}
#app {
  text-align: center;
  padding: 40px 0;
}
</style>
