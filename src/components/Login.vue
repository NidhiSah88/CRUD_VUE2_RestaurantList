<template>
<div>
    <img alt="logo" class="logo" src="../assets/logo3.jpg">
    <h1> Login </h1>
    <div class="login">
        <input type="text" v-model="email"  placeholder="Email"/>
        <input type="password" v-model="password"  placeholder="Password"/>
        <button type="button" v-on:click="login()" >Login</button>
        <p>
            <router-link to="/Sign-Up">Sign Up </router-link>
        </p>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default{
    name:'Login',
    data(){
        return{
            email:'',
            password:''
        }
    },
    methods:{
        async login(){
            console.log(this.email, this.password)
            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`)
            
            if(result.status==200 && result.data.length>0){
                
            localStorage.setItem("user-info",JSON.stringify(result.data[0]))
            this.$router.push({name:"Home"})
            }
            
            console.log(result)
        }
    }

}

</script>

<style scoped>


</style>