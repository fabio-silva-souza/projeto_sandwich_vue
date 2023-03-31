<template>
    <div>
        <h1>Make your Sandwich-ich !</h1>
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
        background-image: url('https://holyschnitzel.com/wp-content/uploads/2018/06/Menu-Page-Banners-1920x765-panini-and-veggie-sandwiches.jpg');
        background-size: cover;
        height: 500px;
    }
    h1
    {
        color: #fff;
        text-align: center;
        font-size: 60px;
        background-color: rgba(0, 0, 0, 0.338);
        border-radius: 20px;
        padding: .2em;
    }
    
</style>