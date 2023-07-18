<template>
    <div class="paes-menu"></div>
    <h1>Recheios</h1>
    <div class="recheios-menu"></div>
    <h1>Opcionias</h1>
    <div class="opcionais"></div>
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
//add function
            let menuPaes = data.paes;
            let paesContainer = '<h2 for="pao">Escolha seu pão :</h2>';

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

//add function
            let menuRecheios = data.recheios;
            let recheiosContainer = '<h2 for="pao">Escolha seu recheio :</h2>';

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

//add function

            let opcionais = data.opcionais;
            let opcionaisContainer = '';

            for ( let i = 0; i < opcionais.length; i++ ) {
                const options = opcionais[i];
                
                const {tipo} = options
          
                const menuO = 
                `  <label class="label-options">
                    <input type="checkbox" class="option-input checkbox" checked />
                    ${tipo}
                  </label>
                `;
               opcionaisContainer += menuO;
            }
            document.querySelector('.opcionais').innerHTML = opcionaisContainer;
          
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
        align-items: center;
        justify-content: space-around;

        margin-bottom: 30px;
        background-color: #292929;
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
        background-color: #454545;
        box-shadow: rgba(50, 50, 93, 0.25) 0px 30px 60px -12px inset, rgba(0, 0, 0, 0.3) 0px 18px 36px -18px inset;
        overflow: hidden;
        transition: 0.5s;
    }
     .bread-img
    {
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
        
        transition: 0.5s;
    }
    h2
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
        position: relative;
        width: 100%;
        height: 50vh;
        background-color: #363036;
        display: flex;
        align-items: center;
        justify-content: space-around;
    }
    .card-recheios
    {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 190px;

        border-radius: 5px;
        border-top-left-radius: 50%;
        border-top-right-radius: 50%;
        border: 1px solid #1C1C1C;
        background: #363036;
        box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
        
        padding-bottom: 15px;
        transition: 0.5s;
    }
    .filling-img
    {
        width: 185px;
        margin-bottom: 15px;
        border-radius: 50%;

        transition: 0.5s;
    }



    .opcionais
    {
        display: grid;
        grid-template-columns: auto auto;
        align-items: center;
        justify-content: space-around;
    }
    h1
    {
        font-size:28px;
        line-height:28px;
        margin: 25px;
    }
    .label-options
    {
        display:block;
        line-height:40px;
    }
    .option-input 
    {
        -webkit-appearance: none;
        -moz-appearance: none;
        -ms-appearance: none;
        -o-appearance: none;
        appearance: none;
        position: relative;
        top: 13.33333px;
        right: 0;
        bottom: 0;
        left: 0;
        height: 40px;
        width: 40px;
        transition: all 0.15s ease-out 0s;
        background: #cbd1d8;
        border: none;
        color: #fff;
        cursor: pointer;
        display: inline-block;
        margin-right: 0.5rem;
        outline: none;
        position: relative;
        z-index: 1000;
    }
    .option-input:hover 
    {
        background: #e9f3ff;
    }
    .option-input:checked 
    {
        background: #00AD11;
    }
    .option-input:checked::before 
    {
        width: 40px;
        height: 40px;
        display:flex;
        content: '\f00c';
        font-size: 25px;
        font-weight:bold;
        position: absolute;
        align-items:center;
        justify-content:center;
        font-family:'';
    }
    .option-input:checked::after 
    {
        -webkit-animation: click-wave 0.65s;
        -moz-animation: click-wave 0.65s;
        animation: click-wave 0.65s;
        background: #00AD11;
        content: '';
        display: block;
        position: relative;
        z-index: 100;
    }

    @keyframes click-wave {
    0% 
    {
        height: 40px;
        width: 40px;
        opacity: 0.35;
        position: relative;
    }
    100% 
    {
        height: 200px;
        width: 200px;
        margin-left: -80px;
        margin-top: -80px;
        opacity: 0;
    }
    }


</style>