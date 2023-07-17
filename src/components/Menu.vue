<template>
    <div class="paes-menu"></div>
    <div class="recheios-menu">
        <h1>TESTE</h1>
    </div>
    <!-- <div class="input-container">
    <label for="pao">Escolha seu pão:</label>
    <select name="pao" id="pao" v-model="pao">
    <option value="">Selecione o seu pão</option>
    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
    {{ pao.tipo }}
    </option>
    </select>    
    </div> -->
</template>

<script>
export default {
    name: 'Menu',
    props: {
        
    },
    methods: {
        async renderMenuOptions() {
            const req = await fetch('http://localhost:3000/ingredientes');
            const data = await req.json();
            
            let menuPaes = data.paes;
            let paesContainer = '<label for="pao">Escolha seu pão :</label>';

            for ( let i = 0; i < menuPaes.length; i++ ) {
                const optionsPaes = menuPaes[i];

                const {tipo} = optionsPaes
                const menuP = 
                `<div class="card">
                   <img src="/imgs/${tipo.toLowerCase()}-pao.png"
                   width="300" class="bread-img">
                  <span class="bread-type">${tipo}</span>
                 </div>
                `;

                paesContainer += menuP;
            }
            document.querySelector('.paes-menu').innerHTML = paesContainer;

            let menuRecheios = data.recheios;
            let recheiosContainer = '<label for="pao">Escolha seu recheio :</label>';

            for ( let i = 0; i < menuRecheios.length; i++ ) {
                const optionsRecheios = menuRecheios[i];

                const {tipo, descricao} = optionsRecheios;
                const menuR = 
                `<div class="card-recheios">
                    <img src="./imgs/${tipo.toLowerCase()}-recheio.png" class="filling-img">
                  <span>${tipo}</span>
                  <span>${descricao}</span>
                 </div>
                `;

                recheiosContainer += menuR;
            }
            document.querySelector('.recheios-menu').innerHTML = recheiosContainer;
        }
    },
    mounted() {
        this.renderMenuOptions();
    }
}
</script>

<style>
    .paes-menu
    {
        display: grid;
        grid-template-columns: auto auto;

        position: relative;
        padding-top: 40px;
        width: 100%;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-around;

        
        box-shadow: 10px 10px 10px 15px #1c1c1c;
        margin-bottom: 30px;
        /* overflow-x: scroll; */
    }
    .card
    {
        display: flex;
        position: relative;
        align-items: center;
        justify-content: center;
        margin: 25px;
        width: 330px;
        height: 230px;
        border-radius: 5px;
        border: 2px solid white;
        overflow: hidden;
        transition: 0.5s;
    }
     .bread-img
    {
        box-shadow: 15px 15px 15px 30px rgba(0, 0, 0, 0.505);
        border-radius: 5px;
        transition: 0.5s;
    }
    .bread-img:hover
    {
        filter: grayscale(100%);
        transition: 0.5s;
    }
    .card:hover 
    {
        border: 2px solid green;
        transition: 0.5s;
    }
    label
    {
        font-size: 30px;
        margin: 10px;
        top: 0;
        color: aliceblue;
        position: absolute;
    }
    .bread-type
    {
        font-size: 20px;
        font-family: 'Caprasimo', cursive;
        color: aliceblue;
        position: absolute;
        bottom: 2px;
        background-color: #1c1c1c;
        padding: 5px 150px;
    }

    .recheios-menu
    {
        width: 100%;
        height: 50vh;
        background-color: #303030a9;
        display: flex;
        align-items: center;
        justify-content: space-around;
    }
    .card-recheios
    {
        display: flex;
        flex-direction: column;
        align-items: center;

        border-radius: 5px;
        border-top-left-radius: 50%;
        border-top-right-radius: 50%;
        border: 2px solid white;
        
        padding-bottom: 15px;
        transition: 0.5s;
    }
    .filling-img
    {
      width: 150px;
      border-radius: 50%;
      transition: 0.5s;
    }

</style>