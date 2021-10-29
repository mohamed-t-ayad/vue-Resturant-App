<template>
    <div>
        <Header />
        <div class="container">
            <div class="row">
                <h1>Home page</h1>
                <table class="table table-hover w-75 m-auto">
                    <thead class="table-dark">
                        <tr>
                        <th scope="col">#</th>
                        <th scope="col">Resturant Name</th>
                        <th scope="col">Address</th>
                        <th scope="col">Contact</th>
                        <th scope="col">Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in resturant" :key="item.id">
                            <th scope="row">{{item.id}}</th>
                            <td>{{item.name}}</td>
                            <td>{{item.address}}</td>
                            <td>{{item.contact}}</td>
                            <td>
                                <router-link :to="'/update/'+item.id" class="btn btn-block btn-info">edit</router-link>
                                <button v-on:click="deleteResturant(item.id)" class="btn btn-danger mx-2">delete</button>
                            </td>
                        </tr>
                    </tbody>
                    <router-link to="/add/" class="btn btn-primary mt-1">Add New Resturant</router-link>
                </table>
            </div>
        </div>
    </div>
</template>
<script>
import Header from './Header.vue';
import axios from 'axios'

export default {
  components: { Header },
    name:'Home',
    data() {
        return {
            name:'',
            resturant:[],
        }
    },
    component:{
        Header
    },
    methods: {
        async deleteResturant(id){
            let result  = await axios.delete("http://localhost:3000/resturants/"+id);
            if (result.status == 200) {
                this.loadData();
            }
        },
        async loadData(){
            let user = localStorage.getItem('user-info');
            this.name = JSON.parse(user).name;
            if(!user){
                this.$router.push({name:'SignUp'})
            }
            let result = await axios.get("http://localhost:3000/resturants");
            this.resturant=result.data;
        }
    },
    async mounted() {
        this.loadData();
    }
}
</script>