<template>
    <nav>
        <router-link to="/" id="logo">
            <img :src="logo" :alt="alt">-ich
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
        background-color: #666;
        border-bottom: 4px solid #111;
        padding: 15px 50px;
    }
    nav a
    {
        color: chartreuse;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }
    nav a:hover
    {
        color: aliceblue;
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