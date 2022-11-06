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
<td><router-link :to="'/update/'+item.id">Update</router-link>
<button v-on:click="deleteRestaurant(item.id)">Delete</button>
</td>
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
    methods:{
        async deleteRestaurant(id)
        {
            let result = await axios.delete("http://localhost:3000/restaurant/"+id);
            console.warn(result);
            if(result.status == 200)
            {
                this.loadData();
            }
        },

   async loadData()
      { 
        let user = localStorage.getItem("user-info");
        this.name = JSON.parse(user).name
        if (!user) {
            this.$router.push({ name: "SignupView" });
        }
        let result = await axios.get("http://localhost:3000/restaurant");
        console.warn(result);
        this.restaurants = result.data

    }
},

   async mounted() {
          this.loadData();
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
