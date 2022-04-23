<template>
<div>

<div class="nav">
<router-link to="/">Home </router-link>
<router-link to="/add">Add Restaurant </router-link>
<router-link to="/update">Update Restaurant </router-link>
<a href="#" v-on:click="logout()">Logout </a>
</div>

</div>
</template>

<script>
export default{
name:'Header',
methods:{
    logout(){
        console.log('logout');
        localStorage.clear()
        this.$router.push({name:'Login'})

    }
}


}

</script>

<style scoped>
.nav{
    overflow:hidden;
    background-color:#333;
}
.nav a{
float:left;
color:#f2f2f2;
padding: 14px 16px;
text-align:center;
font-size:17px;
text-decoration:none;
margin-right:5px;
}
.nav a:hover{
    background-color:#ddd;
    color:#333;
}

</style>