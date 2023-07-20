<template>
    <select class="paes-menu" name="pao" id="pao"></select>
        <h1>Recheios</h1>
    <div class="recheios-menu"></div>
        <h1>Opcionias</h1>
    <div class="opcionais"></div>
    <div class="input-name">
        <h2 for="userName">Nome do cliente:</h2>
            <input type="text" id="userName" name="userName" v-model="userName" placeholder="Digite o seu nome">
        </div>
</template>

<script>
export default {
    name: 'Menu',
    props: {
        
    },
    data(){
        return {
            paes: null,
            recheios: null,
            opcionaisdata: null,
            pao: null,
            recheio: null,
            opcionais: [],          
        }
    },
    methods: {
        async getIngredientes() {

            const req = await fetch('http://localhost:3000/ingredientes');
            const data = await req.json();

            this.paes = data.paes;
            this.recheios = data.recheios;
            this.opcionaisdata = data.opcionais;
        // },
        // renderMenuOptions() {
            // const req = await fetch('http://localhost:3000/ingredientes');
            // const data = await req.json();

// render bread
            // renderBread() {
            let menuPaes = this.paes;
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
            // },
// render flling   
            // renderFilling() {         
            let menuRecheios = this.recheios;
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
            // },
//render options
            // renderOptions() {
            let opcionais = this.opcionaisdata;
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
        this.getIngredientes();
        // this.renderMenuOptions();
        // this.renderBread();
        // this.renderFilling();
        // this.renderOptions();
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
    .filling-img:hover,
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
        font-size: 20px;
        margin: 10px;
        top: 0;
        left: 0;
        color: aliceblue;
        padding: 5px 10px;
        border-left: 4px solid chartreuse;
        position: absolute;
    }
    .bread-type
    {
        font-size: 20px;
        font-family: 'Caprasimo', cursive;
        color: aliceblue;
        position: absolute;
        bottom: 0;
        background-color: #1c1c1c;
        padding: 5px 150px;
    }

    .recheios-menu
    {
        position: relative;
        width: 100%;
        height: 55vh;
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
        width: 80%;
        grid-template-columns: auto auto;
        align-items: center;
        justify-content: space-around;
    }
    h1
    {
        font-size: 35px;
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
        /* content: '🔘'; */
        font-size: 25px;
        font-weight:bold;
        position: absolute;
        align-items:center;
        justify-content:center;
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

    input
    {
        padding: 5px 10px;
        width: 300px;
    }

    .input-name
    {
        display: flex;
        flex-direction: column;
        position: relative;
        margin: 50px 0;
        width: 100%;
        height: 200px;
        background-color: #292929;
        align-items: center;
        justify-content: center;
    }


</style>