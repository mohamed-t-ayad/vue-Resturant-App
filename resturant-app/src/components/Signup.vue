<template>
    <div class="container">
        <div class="logo w-25 m-auto">
            <img src="../assets/logo2.png" alt="Logo" class="d-block m-auto" width="150" height="150">
        </div>
        <h2 class="text-primary py-2 my-2">Sign UP</h2>
        <div class="w-25 m-auto">
            <div class="row">
                <div class="col-12 mb-2">
                    <input type="text" class="form-control p-2" placeholder="Name" v-model="name">
                </div>
                <div class="col-12 mb-2">
                    <input type="email" class="form-control p-2" placeholder="E-mail" v-model="email">
                </div>
                <div class="col-12 mb-2">
                    <input type="password" class="form-control p-2" placeholder="Password" v-model="password">
                </div>
                <div class="col-12 mb-2">
                    <button class="btn btn-block btn-primary" v-on:click="signUp">Sign UP</button>
                </div>
                <div class="col-12 mb-2">
                    <p>Or 
                        <router-link to="/login">Login</router-link> to your account.
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name : 'SignUp',
    data() {
        return {
            name:'',
            email:'',
            password:''
        }
    },
    methods:{
        // async signUP()
        // {
        //     let result = await axios.post("http://localhost:3000/user",{
        //         name:this.name,
        //         email:this.email,
        //         password:this.password
        //     });
        //     console.warn(result);
        //     if(result.status==201) {
        //         alert("signup done");
        //         //localStorage.setItem("user-info" ,JSON.stringify(result.data));
        //     } 
        // }
        async signUp(){
            let result = await axios.post("http://localhost:3000/user",{
                name:this.name,
                email:this.email,
                password:this.password
            });
            console.warn(result);
            if(result.status==201) {
                localStorage.setItem("user-info" ,JSON.stringify(result.data));
                this.$router.push({name:'Home'})
            }
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
<style scoped>

img {
    background-color: transparent;
}
</style>