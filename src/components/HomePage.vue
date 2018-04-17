<template>
  <div>
    <div v-if="loggedIn">
      <main-page/>
    </div>
    <div v-else>
      <welcome-page/>
    </div>
  </div>
</template>

<script>
 import WelcomePage from './WelcomePage';
 import MainPage from './MainPage';
 //import { store } from './../store.js';
 //UserFeed was changed to Main
 export default {
   name: 'HomePage',
   components: {WelcomePage,MainPage},
   computed: {
     loggedIn: function() {
       return this.$store.getters.loggedIn;
     },
   }
 }
</script>

<style scoped>
</style>
