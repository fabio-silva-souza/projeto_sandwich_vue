<template>
    <nav>
        <router-link to="/" id="logo">
            <img :src="logo" :alt="alt">Lanches
        </router-link>
    <router-link to="/">Home</router-link> 
    <router-link to="/pedidos">Pedidos</router-link>
  </nav>
</template>

<script>
export default {
    name: 'Navbar',
    props: ["logo", "alt"]
}
</script>

<style scoped>
    nav
    {
        display: flex;
        justify-content: flex-end;
        align-items: center;
        background-color: #00000000;
        border-bottom: 4px solid #111;
        padding: 15px 50px;
    }
    nav a
    {
        color: rgba(128, 255, 0, 0.753);
        text-decoration: none;
        margin: 12px;
        transition: .5s;
        font-family: 'Caprasimo', cursive;
        font-weight: 200;
        font-size: 18px;
    }
    nav a:hover
    {
        color: rgb(255, 255, 255);
    }
    img
    {
        width: 10%;
    }
    #logo
    {
        margin: auto;
        margin-left: 0;  
    }
</style>