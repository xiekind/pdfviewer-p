<template>
    <div id="app">
        <link href="https://cdn.jsdelivr.net/npm/vuetify@1.2.2/dist/vuetify.min.css" rel="stylesheet" />
        <v-container bg fill-height grid-list-md text-xs-center>
            <v-layout row wrap align-center>
                <v-flex>
                    <h1>This is Home.vue Page</h1>
                        <router-link to="/login">Login</router-link>
                        <router-link to="/register">Register</router-link>
                </v-flex>
            </v-layout>
        </v-container>
    </div>
</template>

<script>
import Login from './forms/Login'

export default {
    components : {
        Login
    },
    methods : {
        login() {
            console.log('login')
        },
        register(){
            console.log('register')
        }
    }
}

</script>

<style scoped>
.btn {
    width: 2rem;
}
</style>
