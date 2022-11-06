<template>
    <HeaderView />
    <h1>Hello, Welcome To Our Add Restaurant Page</h1>
  <form class="add">
    <input type="text" name="name" placeholder="Enter Name" v-model="restaurant.name" />
    <input type="text" name="address" placeholder="Enter Address"  v-model="restaurant.address" />
    <input type="text" name="contact" placeholder="Enter Contact"  v-model="restaurant.contact" />
    <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>

</form>
    
</template>
    
    
    <script>
    import HeaderView from './HeaderView.vue'
    import axios from 'axios'
    
    export default {
        name: "AddView",
        data(){
            return{
                restaurant:{
                    name:'',
                    address:'',
                    contact:''
                }
            }
        },
        methods:{
            async addRestaurant(){
                console.warn(this.restaurant)
                const result = await axios.post("http://localhost:3000/restaurant",{
                    name:this.restaurant.name,
                    address:this.restaurant.result,
                    contact:this.restaurant.contact
                });
                if(result.status == 201)
                {
                    this.$router.push({name:'HomeView'})
                }
                console.warn("result", result)
            }
        },
        mounted() {
            let user = localStorage.getItem("user-info");
            if (!user) {
                this.$router.push({ name: "SignupView" });
            }
        },
        components: {
             HeaderView 
            },
    }
    
    </script>