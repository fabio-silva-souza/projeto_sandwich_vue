<template>
    <div>
        <h1> V lanches !</h1>
    </div>
</template>

<script>
export default {
    name: "Banner"
}
</script>

<style scoped>
    div
    {
        display: flex;
        align-items: center;
        justify-content: flex-start;
        background-image: url('https://images.pexels.com/photos/1565982/pexels-photo-1565982.jpeg?cs=srgb&dl=bread-color-copyspace-1565982.jpg&fm=jpg');
        background-size: cover;
        height: 500px;
    }
    h1
    {
        color: #ffffff;
        font-family: 'Caprasimo', cursive;
        text-align: center;
        font-size: 70px;
        font-weight: 300;
        background-color: rgba(0, 0, 0, 0.548);
        border-radius: 5px;
        padding: .2em;
    }
    img
    {
        width: 300px;
    }
    
</style>