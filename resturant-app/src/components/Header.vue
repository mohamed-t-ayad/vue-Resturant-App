<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-black mb-5">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">
            <img src="../assets/logo2.png" alt="Logo" class="m-auto" width="50" height="50">
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav m-auto mb-2 mb-lg-0">
                <li class="nav-item">
                    <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
                </li>
                <li class="nav-item">
                    <router-link class="nav-link" to="/add">Add Resturant</router-link>
                </li>
                <li class="nav-item">
                    <a class="nav-link" v-on:click="logout" href="#">Log out</a>
                </li>
            </ul>
        </div>
    </div>
    </nav>
</template>
<script>
export default {
    name:'Header',
    methods: {
        logout(){
            localStorage.clear();
            this.$router.push({name:'login'})
        }
    },
}
</script>
<style scoped>
.nav-item {
    padding: 4px 8px ;
}
</style>