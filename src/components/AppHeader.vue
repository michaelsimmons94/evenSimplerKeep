<template>
   <v-toolbar>

    <v-toolbar-title><div class ='title'>Even Simpler Keep</div></v-toolbar-title>
    <v-spacer></v-spacer>
      <div v-if="loggedIn">
        <v-toolbar-items>
       <v-btn v-if="loggedIn" @click="logout" flat>Logout</v-btn> 
     </v-toolbar-items>
      </div>
      <div v-else>
        <v-toolbar-items>
      <v-text-field 
        v-model="email" 
        placeholder="Email Address"
        single-line>
        </v-text-field>
        <v-text-field
        v-model="password"
        placeholder="Password" 

        type= "password" single-line>  
        </v-text-field>

        <v-btn @click.prevent="login" flat> Log In</v-btn>
      </v-toolbar-items>
      </div>
       <v-alert v-if="loginError" type="error" v-model="alert" dismissible >
      {{loginError}}
    </v-alert>
    </v-toolbar>
  

</template>
<script>
 export default {
   name: 'AppHeader',
   data () {
     return {
       email: '',
       password: '',
       alert: true
     }
   },
   computed: {
     user: function() {
       return this.$store.getters.user;
     },
     loggedIn: function() {
       return this.$store.getters.loggedIn;
     },
     loginError: function() {
       return this.$store.getters.loginError;
     },
   },
   methods: {
     login: function() {
       this.$store.dispatch('login',{
         email: this.email,
         password: this.password,
       }).then(user => {
   this.email = '';
   this.password = '';
       });
     },
     logout: function() {
       this.$store.dispatch('logout');
     }
   }
 }
</script>
<style scoped>
 /* Strip the ul of padding and list styling */
 nav {
     display: grid;
     margin-bottom: 20px;
 }
 ul {
     list-style-type:none;
     margin:0;
     padding:0;
 }
 /* Create a horizontal list with spacing */
 li {
     display:inline-block;
     float: left;
     margin-right: 20px;
     height: 50px;
     text-align: center;
     line-height: 50px;
     color: #666;
 }
 /*Active color*/
 li a.active {
 }
 /*Hover state for top level links*/
 li:hover a {
 }
 .right {
     float: right;
 }
 .errorPlace {
     height: 20px;
 }
 img {
     width: 50px;
 }
 .title{
  font-family: 'Pacifico', cursive;
  color:dodgerblue;
 }
</style>