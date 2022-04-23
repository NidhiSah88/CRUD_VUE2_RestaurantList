<template>
<div>
    <Header/>
    <h1>Hello {{name}}, WELCOME to Home </h1>
    <table border="1">
    <tr>
      <td>ID </td>
      <td>NAME</td>
      <td>CONTACT </td>
      <td>ADDRESS</td>
      <td>Actions</td>
    </tr>
    <tr v-for="item in restaurant" :key="item.id">
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.contact}}</td>
      <td>{{item.address}}</td>
      <td><router-link :to="'/update/'+item.id">Update</router-link>
      <button type="button" v-on:click="deleteRest(item.id)">Delete</button>
      </td>
    </tr>
    </table>
    
</div>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';

export default {
  name: 'Home',
  data(){
    return{
      name:'',
      restaurant:[],

    }
  },
  components:{
    Header,

  },
  methods:{
    async deleteRest(id){
      console.log(id)
      let result = await axios.delete("http://localhost:3000/restaurant/"+id);
      console.log("Deleted result", result)
      if(result.status==200){
        this.loadData();
      }
    },
    async loadData(){
      let user = localStorage.getItem('user-info');
      this.name=JSON.parse(user).name;
      if(!user){
        this.$router.push({name:'SignUp'})
      }
      let result = await axios.get("http://localhost:3000/restaurant");
      console.log(result)
      this.restaurant=result.data;

    }
    
  },
  async mounted(){
    this.loadData();
  }

}

</script>
<style scoped>
td{
  width:140px;
  height:40px;
}

</style>
