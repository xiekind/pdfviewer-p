<template>
  <div>
    <link href="https://cdn.jsdelivr.net/npm/vuetify@1.2.2/dist/vuetify.min.css" rel="stylesheet" />
    <v-container bg fill-height grid-list-md text-xs-center>
        <v-layout row wrap align-center>
            <v-flex>   
              <v-card class="mx-auto mt-10 text-center pa-10" 
              elevation="11"
              outlined max-width="600px">
                <v-card-title class="justify-center ">Login</v-card-title>
                <v-card-text>
                  <p class="red--text" v-if="errorMessage !== null">{{errorMessage}}</p>
                  <v-form ref="form" v-model="valid" :lazy-validation="lazy" @submit="login">
                    <v-text-field
                      v-model="email"
                      :rules="emailRules"
                      outlined
                      label="Email"
                      name="email"
                      color="light-blue accent-4"
                      clearable
                      type="email"
                    />
                    <v-text-field
                      :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
                      :rules="passwordRules"
                      :type="show ? 'text' : 'password'"
                      v-model="password"
                      name="password"
                      color="light-blue accent-4"
                      outlined
                      label="Password"
                      required
                      @click:append="show = !show"
                    ></v-text-field>
                    <v-spacer/>
                    <v-card-actions class="justify-center pl-8 pr-8">
                      <v-row class="justify-center "> 
                        <v-icon left>mdi-arrow-right</v-icon>
                        <v-btn
                          class="px-10"
                          dark
                          v-on:click="login()"
                          text-center
                          block
                          color="#0e3da1"
                        >Login</v-btn>
                        <p>don't have an account yet click <a href="register" class="body-2 black--text"><b>HERE</b></a> to create account</p>
                      </v-row>
                    </v-card-actions>
                  </v-form>
                </v-card-text>
              </v-card> 
            </v-flex>
        </v-layout>
    </v-container>
  </div>
</template>

<style scoped>
h2, h1 {
  color: white;
  text-align: center;
}
#back {
  background-color:  white;
  background-size: cover;
}
.card{
  width: 1440px;
  height: 100vh;
}
.loginLayout {
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
}
p {
  text-align: center;
  padding: 5px;
}

</style>
<script>

import axios from 'axios'
export default {
  name: "btnLogin",
  components: {    
  },
  data() {
    return {
      show: false,
      data: false,
      disable: false,
      loginbtn: true,
      valid: true,
      lazy: false,
      email: '',
      password: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
      passwordRules: [v => !!v || "Password is required"],
      errorMessage: null,
    };
  },
  methods: {
    login() {
      if(this.$refs.form.validate()) {
        let parameter = {
          email: this.email,
          password: this.password
        }
        axios.post('/loginsubmit', parameter).then(response => {
          if(response.data.status === true) {
            this.errorMessage = null
            localStorage.setItem('token', true)
            this.$router.push('/dashboard')
          } else {
            console.log(response.data.status)
            this.errorMessage = 'Username and password did not match!'
          }
        })
      console.log('login')
      } else {
        this.errorMessage = 'All fields required!'
      console.log('login error')
      }
    },
  },
  mounted() {}
};
</script>
