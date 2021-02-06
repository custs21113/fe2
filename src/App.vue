<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <router-view/>
  </div>
</template>

<script>
import Container from '@/page/Container'
export default {
  name: 'App',
  componen: {
    Container
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 50px;
  /* padding-bottom: 60px; */
  /* background-repeat: 1; */
}
html {
  background-image: url('./assets/bg.png');
  background-size: 100%;
}
</style>
