<template>

<div class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="/add">Add Restaurant</router-link>
  
    <a v-on:click="logout" href="#">Logout</a>

</div>
</template>

<script>
export default {
    name:'HeaderView',
    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name:'LoginView'})
        }
    }
}
</script>

<style>
.nav{
    background-color: #333;
    overflow: hidden;
}

.nav a{
    float:left;
    color: #f2f2f2;
    padding: 16px 20px;
    text-decoration: none;
    font-size: 16px;
    margin-right: 4px;
    text-align: center;
}
.nav a:hover{
    background-color: #ddd;
    color:#222;
}
</style>