<template>
    <div class="container">
        <div class="logo w-25 m-auto">
            <img src="../assets/logo2.png" alt="Logo" class="d-block m-auto" width="150" height="150">
        </div>
        <h2 class="text-primary my-2 p-4">Login</h2>
        <div class="w-25 m-auto">
            <div class="row">
                <div class="col-12 mb-3">
                    <input type="email" class="form-control p-2" placeholder="E-mail" v-model="email">
                </div>
                <div class="col-12 mb-2">
                    <input type="password" class="form-control p-2" placeholder="Password" v-model="password">
                </div>
                <div class="col-12 mb-3">
                    <button class="btn btn-block btn-primary" v-on:click="login">Login</button>
                </div>
                <div class="col-12 mb-2">
                    <p>don't have account
                        <router-link to="/signup">Create new account </router-link>.
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'Login',
    data() {
        return {
            email:'',
            password:''
        }
    },
methods: {
    async login(){
        let result = await axios.get(`http://localhost:3000/users?email${this.email}=&password=${this.password}`)
        if(result.status==200 && result.data.length>0) {
                localStorage.setItem("user-info" ,JSON.stringify(result.data));
                this.$router.push({name:'Home'})
            }
        console.log(this.email,this.password)
    }
},
mounted() {
        let user = localStorage.getItem('user-info');
        if(user){
            this.$router.push({name:'Home'})
        }
    },
}
</script>