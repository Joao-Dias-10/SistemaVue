<template>
  <div id="nav">
    <router-link to="/" id="logo-url" >
      <img :src="logo" :alt="alt" id="logo" />
    </router-link>
    <router-link to="/">Home </router-link>
    <router-link to="/Pedidos">Pedidos</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"]
};
</script>


<style scoped>
#nav{
  background-color:  #ff1717;
  border-bottom: 1px solid  #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
#logo{
width: 40px;
height: 40px;
}
#nav #logo-url{
margin: auto;
margin-left: 0;
}
#nav a{
  color: #ffffff;
  text-decoration: none;
  margin: 12px;
  transition: .5s;
}
#nav a:hover{
  color: #454545;
 
}
</style>