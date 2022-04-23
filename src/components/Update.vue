<template>
<div>
<Header/>
<h2>Welcome to Update Restaurant Page</h2>
<form class="addres">
<input type="text"  placeholder="Enter Name" v-model="restaurant.name"/>
<input type="text"  placeholder="Enter Address" v-model="restaurant.address"/>
<input type="text"  placeholder="Enter Contact" v-model="restaurant.contact"/>
<button type="button" v-on:click="updateRest()" >Update new Restaurant </button>
</form>

</div>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';

export default{
    name:'Update',
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
    async updateRest(){
      console.log(this.restaurant)
      let result = await axios.put('http://localhost:3000/restaurant/'+this.$route.params.id,{
        name:this.restaurant.name,
        address:this.restaurant.address,
        contact:this.restaurant.contact
      })
      if(result.status==200){
        
        this.$router.push({name:"Home"})
      }
      console.log("put Result", result);

    }
  },
  async mounted(){
    let user = localStorage.getItem('user-info');
    if(!user){
      this.$router.push({name:'SignUp'})
    }
    let result = await axios.get('http://localhost:3000/restaurant/'+this.$route.params.id)
    console.log(this.$route.params.id);
    console.log("Result is:", result);
    this.restaurant=result.data;
  }

}

</script>

<style scoped>



</style>