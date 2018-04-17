<template>
  <v-app>
    <div id="app">
    <app-header></app-header>
    <router-view/>
  </div>
  </v-app>
</template>

<script>
import AppHeader from './components/AppHeader';
export default {
 
  name: 'App',
  components: {AppHeader}
}
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: dodgerblue;
}
h1{
  font-family: 'Pacifico', cursive;
  color:white;
  font-size: 4em;
}
h3{
  color:white;
  font-size: 1.5em;
}
</style>
