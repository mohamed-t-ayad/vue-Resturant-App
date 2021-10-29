<template>
    <div>
        <Header />
        <div class="container">
            <h1>Add New Resturant</h1>
            <form action="" class="w-50 m-auto">
                <input class="form-control mb-3" type="text" v-model="resturant.name" placeholder="Resturant Name">
                <input class="form-control mb-3" type="text" v-model="resturant.address" placeholder="Address">
                <input class="form-control mb-3" type="text" v-model="resturant.contact" placeholder="Contact Number">
                <button class="btn btn-success" v-on:click="addResturant" type="button">Add Resturant</button>
            </form>
        </div>
    </div>
</template>
<script>
import Header from './Header.vue';
import axios from 'axios'
export default {
  components: { Header },
    name:'Add',
    data() {
        return {
            resturant:{
                name:'',
                address:'',
                contact:''
            }
        }
    },
    methods: {
        async addResturant(){ // API's Always async
            console.log(this.resturant)
            const result = await axios.post(" http://localhost:3000/resturants",{
                name:this.resturant.name,
                address:this.resturant.address,
                contact:this.resturant.contact,
            });
            if (result.status == 201) {
                this.$router.push({name:'Home'})
            }
            console.warn("Result" , result)
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if(!user){
            this.$router.push({name:'SignUp'})
        }
    }

}
</script>