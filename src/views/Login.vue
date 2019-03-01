<template>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12">
              <v-toolbar dark color="light-green">
                <v-toolbar-title>Wunder List</v-toolbar-title>
                <v-spacer></v-spacer>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field prepend-icon="person" v-model="email" name="login" label="Login" type="text"></v-text-field>
                  <v-text-field prepend-icon="lock" v-model="password" name="password" label="Password" id="password" type="password"></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click  = "login" >Login</v-btn>
                <v-btn color="primary" @click = "register">Register</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
</template>

<script>
  import firebase from 'firebase';

  export default {
    name: 'login',
    data:() => {
        return{
            email:'',
            password:''
        };
    },
    methods: {
      login: function() {
          firebase.auth().signInWithEmailAndPassword(this.email, this.password).then(
              (user) => {
                  this.$router.replace('home');
              },
              (err) => {
                   alert('Oops. ' + err.message);
              } 
          );
      },
      register: function(){
          this.$router.push('/signUp');
      }
    }
  }
</script>

<style>
  a {
     text-decoration: none;
 }
</style>