<template>
  <v-container grid-list-xl>
   <v-layout row wrap align-center>
    <v-flex xs6 offset-xs3>

      <v-card>
       <div class="title">Register</div>
        
        <v-form ref="form">
          <v-text-field
          label="User Name"
          v-model="username"
          placeholder="User Name"
          required
          ></v-text-field>
          <v-text-field
          label= "Name"
          v-model="name"
          placeholder="First and Last Name"
          required
          >

        </v-text-field>
        <v-text-field
        label="E-mail"
        placeholder="test@test.com"
        v-model="email"
        required
        ></v-text-field>
        <v-text-field
        label= "Password"
        v-model="password"
        type="password"
        placeholder= "Password"
        required>

      </v-text-field>

      <v-btn
      flat
      color="blue"
      @click="register()"
      
      >
      Register
    </v-btn>
  </v-form>
</v-card>
</v-flex>
</v-layout>
</v-container>
</template>
<script>
export default {
 name: 'WelcomePage',
 data () {
   return {
    model: 'tab-2',
    username: '',
    email: '',
    password: '',
    name: '',
  }
},
computed: {
 registerError: function() {
   return this.$store.getters.registerError;
 },
},
methods: {
 register: function() {
  console.log("registered");
   this.$store.dispatch('register',{
     username: this.username,
     email: this.email,
     password: this.password,
     name: this.name,
   });
 },
}
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input{
  color:white;
}
.error{
  color:red;
}
.title{
  color:dodgerblue;
  font-family: Pacifico;
  text-align: center;
  font-size: 2em;
}
</style>

