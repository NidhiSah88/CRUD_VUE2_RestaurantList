<template>
<div>
<Header/>
<h2>Welcome to Add Restaurant Page</h2>
<form class="addres">
<input type="text"  placeholder="Enter Name" v-model="restaurant.name"/>
<input type="text"  placeholder="Enter Address" v-model="restaurant.address"/>
<input type="text"  placeholder="Enter Contact" v-model="restaurant.contact"/>
<button type="button" v-on:click="addRest()" >Add new Restaurant </button>


</form>
</div>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';

export default{
    name:'Add',
    data(){
      return{
        restaurant: {
          name:'',
          address:'',
          contact:''
        }
      }
    },
    components:{
    Header,
    },
    methods: {
      async addRest(){
        console.log(this.restaurant)
        let result = await axios.post("http://localhost:3000/restaurant",{
          name:this.restaurant.name,
          address:this.restaurant.address,
          contact:this.restaurant.contact
        });
        if(result.status==201){
          
          this.$router.push({name:"Home"})
        }
        console.log("Result", result);

      }
    }


}

</script>

<style scoped>



</style>