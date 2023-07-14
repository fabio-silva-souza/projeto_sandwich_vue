<template>
   <div id="lanche-table">
    <message :msg="msg" v-show="msg"/>
    <div>
        <div id="lanche-table-heading">
            <div class="order-id">#:</div>
            <div>Cliente:</div>
            <div>Pão:</div>
            <div>Recheio:</div>
            <div>Opcionais:</div>
            <div>Ações:</div>
        </div>
    </div>
    <div id="lanche-table-rows">
        <div class="lanche-table-row" v-for="lanche in lanches" :key="lanche.id">
            <div class="order-number">{{ lanche.id }}</div>
            <div>{{ lanche.userName }}</div>
            <div>{{ lanche.pao }}</div>
            <div>{{ lanche.recheio }}</div>
            <div>
                <ul>
                    <li v-for="(opcional, index) in lanche.opcionais" :key="index">
                        {{ opcional }}
                    </li>
                </ul>
            </div>
            <div>
                <select name="status" class="status" @change="updatelanche($event, lanche.id)">
                    <option value="">Selecione</option>
                    <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="lanche.status == s.tipo">
                        {{ s.tipo }}
                    </option>
                </select>
                <button class="delete-btn" @click="deletelanche(lanche.id)">Cancelar</button>
            </div>
        </div>
      </div>
   </div>
</template>


<script>
import Message from './Message.vue';

export default {
    name: "Dashboard",
    components: {
        Message
    },
    data() {
        return {
            lanches: null,
            lanche_id: null,
            status: [],
            msg: null
        }
    },
    methods: {
        async getPedidos() {
            const req = await fetch("http://localhost:3000/lanches");

            const data = await req.json();

            this.lanches = data;
        
            this.getStatus();
        },
        async getStatus() {

            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;

        },
        async deletelanche(id) {

            const req = await fetch(`http://localhost:3000/lanches/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            
        // colocar uma msg
        this.msg = `Pedido cancelado com sucesso!`;


        // limpar msg
        setTimeout(() => this.msg = "", 3000);

            this.getPedidos();

        },
        async updatelanche(event, id) {

            const option = event.target.value;

            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`http://localhost:3000/lanches/${id}`, {
                method: "PATCH",
                headers: {"Content-Type" : "application/json" },
                body: dataJson
            });

            const res = await req.json();

            
        // colocar uma msg
        this.msg = `O pedido N° ${res.id} foi atualizado para ${res.status}`;


        // limpar msg
        setTimeout(() => this.msg = "", 3000);
        
        }
    },
    mounted() {
        this.getPedidos();
    }
}
</script>

<style scoped>
    #lanche-table
    {
        max-width: 1200px;
        margin: 0 auto;
    }
    #lanche-table-heading,
    #lanche-table-rows,
    .lanche-table-row
    {
        display: flex;
        flex-wrap: wrap;
    }

    #lanche-table-heading
    {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }

    #lanche-table-heading div,
    .lanche-table-row div
    {
        width: 19%;
    }

    .lanche-table-row 
    {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #lanche-table-heading .order-id,
    .lanche-table-row .order-number
    {
        width: 5%;
    }

    select
    {
        padding: 12px 6px;
        margin-right: 12px;
    }

    .delete-btn
    {
        background-color: #222;
        color: chartreuse;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover 
    {
        background-color: transparent;
        color: #222;
    }

</style>