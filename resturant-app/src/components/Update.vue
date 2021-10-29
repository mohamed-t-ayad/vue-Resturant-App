<template>
    <div>
        <Header />
        <div class="container">
            <h1>Add New Resturant</h1>
            <form action="" class="w-50 m-auto">
                <input class="form-control mb-3" type="text" v-model="resturant.name" placeholder="Resturant Name">
                <input class="form-control mb-3" type="text" v-model="resturant.address" placeholder="Address">
                <input class="form-control mb-3" type="text" v-model="resturant.contact" placeholder="Contact Number">
                <button class="btn btn-info" v-on:click="updateResturant" type="button">Update Resturant</button>
            </form>
        </div>
    </div>
</template>
<script>
import Header from './Header.vue';
import axios from 'axios'

export default {
  components: { Header },
    name:'Update',
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
        async updateResturant(){
            const result = await axios.put(" http://localhost:3000/resturants/"+this.$route.params.id,{
                name:this.resturant.name,
                address:this.resturant.address,
                contact:this.resturant.contact,
            });
            if (result.status == 200) {
                this.$router.push({name:'Home'})
            }
        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        if(!user){
            this.$router.push({name:'SignUp'})
        }
        const result = await axios.get('http://localhost:3000/resturants/'+this.$route.params.id)
        //console.warn(result)
        this.resturant = result.data
    }

}
</script>