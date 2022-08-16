<template>
    <div id="burger-table">
        
        <Message :msg="msg" v-show="msg"></Message>
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
            <div id="burger-table-rows">
                <div id="burger-table-row" v-for="dados in dadosBackend" :key="dados.id">
                    <div class="order-number">{{ dados.id }}</div>
                    <div>{{ dados.nome }}</div>
                    <div>{{ dados.pao }}</div>
                    <div>{{ dados.carne }}</div>
                    <div>
                        <ul>
                            <li v-for="opcionais in dados.opcionais" :key="opcionais">{{ opcionais }}</li>
                        </ul>
                    </div>
                    <div>
                        <select name="status" class="status" @change="updateBurger($event, dados.id)">
                            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="dados.status == s.tipo">{{ s.tipo }}</option>
                        </select>
                        <button @click="deleteBurger(dados.id)" class="delete-btn">Cancelar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';
export default {
    name: "Dashboard",
    data() {
        return {
            nome: null,
            pao: null,
            carne: null,
            nome: null,
            opcionais: [],
            dadosBackend: [],
            status: [],
            msg: null
        };
    },
    methods: {
        async getBurgers() {
            // requisicao feita para o backend
            const req = await fetch("http://localhost:3000/burgers");
            const data = await req.json();
            this.dadosBackend = data;
            // resgatar status 
            this.getStatus();
        },
        async getStatus() {
            const req = await fetch("http://localhost:3000/status");
            const data = await req.json();
            this.status = data;
        },
        async deleteBurger(id) {
            // requisicao feita para o backend
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });
            const res = await req.json();
            // msg de pedido deletado
            this.msg = `Pedido Nº ${id} cancelado com sucesso`;
            setTimeout(() => {
                this.msg = "";
            }, 3000);
            this.getBurgers();
        },
        async updateBurger(event, id) {
            const option = event.target.value;
            const dataJson = JSON.stringify({ status: option });
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });
            const res = await req.json();
        }
    },
    mounted() {
        this.getBurgers();
    },
    components: { Message }
}
</script>

<style scoped>
    #burger-table {
        max-width: 1200px;
        margin: 0 auto;
    }

    #burger-table-heading,
    #burger-table-rows,
    #burger-table-row {
        display: flex;
        flex-wrap: wrap;
    }

    #burger-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }

    #burger-table-heading div,
    #burger-table-row div {
        width: 19%;
    }

    #burger-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #burger-table-heading .order-id, 
    #burger-table-row .order-number {
        width: 5%;
    }

    select {
        padding: 12px 6px;
        margin-right: 12px;
    }

    .delete-btn {
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover {
        background: transparent;
        color: #222;
    }
</style>