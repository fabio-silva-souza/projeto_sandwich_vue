<template>
   <div id="sandwich-table">
    <message :msg="msg" v-show="msg"/>
    <div>
        <div id="sandwich-table-heading">
            <div class="order-id">#:</div>
            <div>Cliente:</div>
            <div>Pão:</div>
            <div>Proteina:</div>
            <div>Opcionais:</div>
            <div>Ações:</div>
        </div>
    </div>
    <div id="sandwich-table-rows">
        <div class="sandwich-table-row" v-for="sandwich in sandwiches" :key="sandwich.id">
            <div class="order-number">{{ sandwich.id }}</div>
            <div>{{ sandwich.userName }}</div>
            <div>{{ sandwich.pao }}</div>
            <div>{{ sandwich.proteina }}</div>
            <div>
                <ul>
                    <li v-for="(opcional, index) in sandwich.opcionais" :key="index">
                        {{ opcional }}
                    </li>
                </ul>
            </div>
            <div>
                <select name="status" class="status" @change="updateSandwich($event, sandwich.id)">
                    <option value="">Selecione</option>
                    <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="sandwich.status == s.tipo">
                        {{ s.tipo }}
                    </option>
                </select>
                <button class="delete-btn" @click="deleteSandwich(sandwich.id)">Cancelar</button>
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
            sandwiches: null,
            sandwich_id: null,
            status: [],
            msg: null
        }
    },
    methods: {
        async getPedidos() {
            const req = await fetch("http://localhost:3000/sandwiches");

            const data = await req.json();

            this.sandwiches = data;
        
            this.getStatus();
        },
        async getStatus() {

            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;

        },
        async deleteSandwich(id) {

            const req = await fetch(`http://localhost:3000/sandwiches/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            
        // colocar uma msg
        this.msg = `Pedido cancelado com sucesso!`;


        // limpar msg
        setTimeout(() => this.msg = "", 3000);

            this.getPedidos();

        },
        async updateSandwich(event, id) {

            const option = event.target.value;

            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`http://localhost:3000/sandwiches/${id}`, {
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
    #sandwich-table
    {
        max-width: 1200px;
        margin: 0 auto;
    }
    #sandwich-table-heading,
    #sandwich-table-rows,
    .sandwich-table-row
    {
        display: flex;
        flex-wrap: wrap;
    }

    #sandwich-table-heading
    {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }

    #sandwich-table-heading div,
    .sandwich-table-row div
    {
        width: 19%;
    }

    .sandwich-table-row 
    {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #sandwich-table-heading .order-id,
    .sandwich-table-row .order-number
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