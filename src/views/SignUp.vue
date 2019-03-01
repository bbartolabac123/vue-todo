<template>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12">
              <v-toolbar dark color="light-green">
                <router-link to = "/login"><v-icon dark left>arrow_back</v-icon> </router-link> 
                <v-toolbar-title>Sign Up Form</v-toolbar-title>
                <v-spacer></v-spacer>
              </v-toolbar>
              <v-card-text>
                   <v-alert
                  :value="alert"
                  color="error"
                  icon="warning_circle"
                  outline
                >
                Please fill all required fields.
                 </v-alert>
                <v-form>
                  <v-text-field prepend-icon="person" v-model="email" name="username" label="Enter your preferred username" type="text"></v-text-field>
                  <v-text-field prepend-icon="lock" v-model="password" name="Pass" label="Enter your preferred Password" id="password" type="password"></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-btn flat color="primary" @click = "register">Register</v-btn>
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
            password:'',
            errors: 'Please fill all fields',
            alert: false
        };
    },
    methods: {
      register: function() {
         if(this.email && this.password) {
            firebase.auth().createUserWithEmailAndPassword(this.email, this.password).then(
              (user) => {
                  this.$router.replace('home');
                },
              (err) => {
                  alert('Oops' + err.message);
              }
           );
         }else{
            this.alert = true;
         }
      }
    }
  }
</script>
