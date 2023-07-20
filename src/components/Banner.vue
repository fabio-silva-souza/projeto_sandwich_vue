<template>
    <div>
        <h1> V lanches faça seu lanche Vegano</h1>
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
        background-image: url('/public/imgs/banner.jpg');
        background-size: cover;
        height: 500px;
        position: relative;
    }
    h1
    {
        position: absolute;
        color: #00AD11;
        font-family: 'Caprasimo', cursive;
        
        font-size: 70px;
        font-weight: 300;
        background-color: rgba(0, 0, 0, 0.548);
        border-radius: 5px;
        padding: .5em;
    }
    
</style>