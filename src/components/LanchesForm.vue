<template>
    <div>
        <message :msg="msg" v-show="msg"/>
        <div>
            <form id="lanche_form" @submit="createlanche">
            
                <menu-v />
                <!-- <div class="input-container">
                    <label for="pao">Escolha seu pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                            {{ pao.tipo }}
                        </option>
                    </select>    
                </div> -->
                <!-- <div class="input-container">
                    <label for="recheios">Escolha sua recheio:</label>
                    <select name="recheio" id="recheio" v-model="recheio">
                        <option value="">Selecione o tipo de recheio</option>
                        <option v-for="recheio in recheios" :key="recheio.id" :value="recheio.tipo">
                            {{ recheio.tipo }}
                        </option>
                    </select>
                </div> -->
                <!-- <div id="opcionais-container" class="input-container">
                    <label id="opcionais-title" for="opcionais">Opcionais:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id" >
                        <input type="checkbox" name="opcionais"  v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                </div> -->
                <!-- <div class="input-name">
                    <label for="userName">Nome do cliente:</label>
                    <input type="text" id="userName" name="userName" v-model="userName" placeholder="Digite o seu nome">
                </div> -->
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu lanche">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import MenuV from './Menu.vue';
import Message from './Message.vue';

export default {
    name: 'LanchesForm' ,
    components: { 
        Message,
        MenuV
    },
    data() {
        return {
            // paes: null,
            // recheios: null,
            // opcionaisdata: null,
            userName: null,
            // pao: null,
            // recheio: null,
            // opcionais: [],
            msg: null           
        }
    },
    methods: {
        // async getIngredientes() {

        //     const req = await fetch('http://localhost:3000/ingredientes');
        //     const data = await req.json();

        //     this.paes = data.paes;
        //     this.recheios = data.recheios;
        //     this.opcionaisdata = data.opcionais;
        // },
        async createlanche(e) {
        
        e.preventDefault(); 
        
        const data = {
            userName: this.userName,
            recheio: this.recheio,
            pao: this.pao,
            opcionais: Array.from(this.opcionais),
            status: "Solicitado"
        }

        const dataJson = JSON.stringify(data);

        const req = await fetch('http://localhost:3000/lanchees', {
            method: "POST",
            headers: { "Content-Type" : "application/json"},
            body: dataJson
        });

        const res = await req.json();

        // colocar uma msg
        this.msg = `Pedido N° ${res.id} realizado com sucesso`


        // limpar msg            
        setTimeout(() => this.msg = "", 3000);

        // limpar os campos
        this.userName = "";
        this.recheio = "";
        this.pao = "";
        this.opcionais = "";
        }
    },
    mounted() {
        this.getIngredientes()
    }
}
</script>

<style scoped>
    #lanche_form
    {
        max-width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    label
    {
        font-weight: bold;
        margin-bottom: 15px;
        color: #fff;
        padding: 5px 10px;
        border-left: 4px solid chartreuse;
    }

    /* input
    {
        padding: 5px 10px;
        width: 300px;
    }

    .input-name
    {
        display: flex;
        flex-direction: column;
        margin: 50px 0;
        width: 100%;
        height: 200px;
        background-color: #292929;
        align-items: center;
        justify-content: center;
    } */

    #opcionais-container
    {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title
    {
        width: 100%;
    }

    /* .checkbox-container
    {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input
    {
        width: auto;
    }

    .checkbox-container span
    {
        margin-left: 6px;
        font-weight: bold;
    } */

    .submit-btn
    {
        background-color: #fff;
        color: chartreuse;
        font-weight: bold;
        border: 2px solid #fff;
        padding: 10px;
        margin: 30px;
        font-size: 16px;
        /* margin: 0 auto; */
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover
    {
        background-color: transparent;
        color: #fff;
    }
</style>