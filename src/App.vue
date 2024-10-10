<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <SchoolList />
</template>

<script>

import SchoolList from './components/SchoolList.vue'

export default {
  name: 'App',
  components: {
    SchoolList
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
 
}
</style>
