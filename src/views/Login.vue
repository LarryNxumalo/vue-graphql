<template>
   <section class="landing">
       <img src="../assets/logo.svg" alt="">
    <form>
        <transition name="fade">
            <!-- <input v-if="toggler" type="text" v-model="name" placeholder="name"> -->
            <input v-if="instruction.register" type="text" v-model="name" placeholder="name">
        </transition>
        <input type="email"  v-model="email" placeholder="email">
        <input type="password" v-model="password" placeholder="password">
        <!-- <button @click.prevent="login">Sign In</button> -->
        <button @click.prevent="submit">Sign In</button>
        <!-- <p @click="togglerUp">Sign Up</p> -->
        <p @click="toggle">Sign Up</p>
    </form>
    </section> 
</template>

<script>
import axios from "axios"
export default {
  watch: {
  },
    data() {
        return {
            toggler: false,
            instruction: {
                login: true,
                register: false
            },
            info: {},
            name: "",
            // sign: {
            //     email: "",
            //     password: ""
            // },
                email: "",
                password: ""
            
        }
    },
    // mounted(){
    //     const {email, password} = this;
    //     axios
    //         .post('https://kasioke.herokuapp.com/user', {email, password})
    //         .then(response => (this.info = response.data))
    //         console.log(this.info)
    // },
    methods: {
        togglerUp () { 
            this.toggler = !this.toggler
        },
        login(){
            //-------------------------
            //Auth
            //403: Password incorrect
            //404: User does not exist
            //200: Successful auth
            //-------------------------
            const { email, password} = this;
            axios
                .post('https://kasioke.herokuapp.com/auth', { email, password })
                // .then(response => (this.info = response.data))
                .then(response => (this.info = response))

                // First log response.
                console.log(this.info);

                // console.log(this.info)
                // //local store
                // let token = this.info.id 
                // let local_token = window.localStorage.setItem("token", token )

                // // console.log(local_token)
                // // console.log(token)
                // alert(window.localStorage.getItem('token'))
                // alert(token);
                
                // if (token === local_token){
                //     console.log('tokens match, keep logged in')
                // } 
        },
        toggle() {
            this.instruction.login = !this.instruction.login;
            this.instruction.register = !this.instruction.register;
            console.log(this.instruction);
        },
        submit() {
            // Login logic
            if(this.instruction.login) {
                const {email, password} = this;
                axios
                .post('http://172.31.11.105:3000/auth', { email, password })
                .then(response => (this.info = response));

                var statusCodes = [200, 204, 404];

                if(statusCodes.indexOf(this.info.status) > -1) {
                    if(this.info.status == 200 || 204) {
                        console.log('logged in successfully.');
                    }

                    if(this.info.status == 404) {
                        console.log('incorrect username of password.')
                    }
                } else {
                    console.log('there was an eror logging you in.', this.info.status);
                }
            }

            // Registration logic
            if(this.instruction.register) {
                const {name, email, password} = this;
                axios
                .post('http://172.31.11.105:3000/user', { name, email, password })
                .then(response => (this.info = response));

                console.log(this.info);
            }
        }
    }
}
</script>

<style>
    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s;
     }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
</style>