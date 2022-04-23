<template>
<div>
    <img alt="logo" class="logo" src="../assets/logo4.jpg">
    <h1> Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name"  placeholder="Name"/>
        <input type="text" v-model="email"  placeholder="Email"/>
        <input type="password" v-model="password"  placeholder="Password"/>
        <button type="button" v-on:click="signUp()" >Sign Up</button>
        <p>
            <router-link to="/login">Login </router-link>
        </p>
    </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'SignUp',
  data(){
    return{
    name:'',
    email:'',
    password:''

    }
  },
  methods:{
   async signUp(){
      
       let result = await axios.post("http://localhost:3000/users",{
           email:this.email,
           password:this.password,
           name:this.name
       })
        
        if(result.status==201){
           
            localStorage.setItem("user-info",JSON.stringify(result.data))
            this.$router.push({name:"Home"})
        }
        console.log(result)
   }

  },
  mounted(){
    let user = localStorage.getItem('user-info');
    if(user){
      this.$router.push({name:'Home'})
    }
  }


}

</script>

<style>


</style>