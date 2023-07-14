<template>
    <div class="options-1"></div>
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
            let vmen = document.querySelector('.options-1').innerHTML = '';
    
            const req = await fetch('http://localhost:3000/ingredientes');
            const data = await req.json();
            let menuPaes = data.paes;

            let menuOptions = '';

            for ( let i = 0;i < menuPaes.lenght; i++ ) {
                const optionsPaes = menuPaes[i];

                const {tipo} = optionsPaes
                const menuV = 
                `<div class="card">
                   <img src="../imgs/${tipo.toLowerCase()}-pao.png" class="bread-img">
                  <span>${tipo}</span>
                 </div>
                `;

                vmen += menuV;
            }
        }
    },
    mounted() {
        this.renderMenuOptions();
    }

}
</script>