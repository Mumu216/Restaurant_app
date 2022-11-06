<template>
<HeaderView />
<h1>Hello {{ name }}, Welcome To Our Home Page</h1>
<div class="container">
    <table border="2px solid">
 <tr>
   <td>ID</td>
   <td>Name</td>
   <td>Address</td>
   <td>Contact</td>
   <td>Action</td>

</tr>
<tr v-for="item in restaurants" :key="item.id">
<td>{{ item.id }}</td>
<td>{{ item.name }}</td>
<td>{{ item.address }}</td>
<td>{{ item.contact }}</td>
<td><router-link :to="'/update/'+item.id">Update</router-link></td>
</tr>
</table>
</div>

</template>


<script>
import axios from 'axios'
import HeaderView from './HeaderView.vue'

export default {
    name: "HomeView",
    data(){
        return{
            name:'',
            restaurants:[]
        }
    },
    async mounted() {
        let user = localStorage.getItem("user-info");
        this.name = JSON.parse(user).name
        if (!user) {
            this.$router.push({ name: "SignupView" });
        }
        let result = await axios.get("http://localhost:3000/restaurant") 
        console.warn(result);
        this.restaurants = result.data
    },
    components: {
         HeaderView 
        },
}

</script>
<style>
td{
   width: 140px;
   height:60px;
   
}
.container{
    margin-left: 250px;
    margin-bottom: 0;
    padding-left: 100px;
    
}
</style>
