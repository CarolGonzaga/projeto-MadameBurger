<template>
    <div>
        <div class="msg-container">
            <Message :msg="msg" v-show="msg" />
        </div>
        <div class="dash-container">
            <div class="card-pedidos" v-for="burger in burgers" :key="burger.id">
                <div class="card-head">
                    <div class="order-id"># {{ burger.id }}</div>
                    <div><strong>Cliente:</strong> {{ burger.nome }}</div>
                </div>
                <div class="card-body">
                    <div class="data-body">
                        <span>Pão:</span>
                        <p>{{ burger.pao }}</p>
                    </div>
                    <div class="data-body">
                        <span>Carne:</span>
                        <p>{{ burger.carne }}</p>
                    </div>
                    <div class="data-body">
                        <span>Molho: </span>
                        <p>{{ burger.molho }}</p>
                    </div>
                    <div class="add-body">
                        <p class="add-body-title">Adicionais:</p>
                        <ul>
                            <li v-for="(opcional, index) in burger.extras" :key="index">
                                {{ opcional }}
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="card-footer">
                    <select name="status" class="status" @change="updateBurger($event, burger.id)">
                        <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">
                            {{ s.tipo }}</option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">
                        <TrashCanIcon />
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import TrashCanIcon from 'vue-material-design-icons/TrashCan.vue';
import Message from './Message.vue';

export default {
    name: "Dashboard",

    components: {
        TrashCanIcon,
        Message
    },

    data() {
        return {
            burgers: null,
            burger_id: null,
            status: [],
            msg: null
        }
    },

    methods: {
        async getPedidos() {
            const req = await fetch('https://api-madameburger-bay.vercel.app/burgers');

            const data = await req.json();

            this.burgers = data;

            //Resgatar o status
            this.getStatus();
        },

        async getStatus() {

            const req = await fetch('https://api-madameburger-bay.vercel.app/status')

            const data = await req.json();

            this.status = data;
        },

        async deleteBurger(id) {

            const req = await fetch(`https://api-madameburger-bay.vercel.app/burgers/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            // Enviando uma mensagem ao usuário
            this.msg = `Pedido removido com sucesso!`

            // Limpar mensagem da tela
            setTimeout(() => this.msg = "", 3000);

            // Atualizar página de pedidos
            this.getPedidos();

        },

        async updateBurger(event, id) {

            const option = event.target.value;

            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`https://api-madameburger-bay.vercel.app/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            // Enviando uma mensagem ao usuário
            this.msg = `O pedido nº ${res.id} foi alterado para ${res.status}!`

            // Limpar mensagem da tela
            setTimeout(() => this.msg = "", 3000);
        }
    },

    mounted() {
        this.getPedidos();
    }
}
</script>

<style scoped>

.msg-container {
    height: 100px;
    text-align: center;
}

.dash-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
}

.card-pedidos {
    background-color: #FFF;
    width: 300px;
    height: 480px;
    margin: 20px;
    padding: 10px;
    border-radius: 5px;
    display: flex;
    flex-direction: column;
    border: 2px solid #917f686b;
    padding: 10px;
}

.card-head {
    background-color: #F0D3AD;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 10px;
    border-radius: 5px;
    border: 2px dotted #917f686b;
}

.order-id {
    text-transform: uppercase;
    font-weight: bold;
    font-size: 20px;
}

.card-body {
    height: 70%;
    margin: 20px 5px;
    border-radius: 5px;
    display: flex;
    flex-direction: column;
    gap: 5px;
}

.data-body {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    font-weight: bold;
}

.data-body p {
    color: #B82E29;
}

.add-body-title {
    font-weight: bold;
    margin: 10px 0;
}

ul {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    gap: 5px;
}

li {
    width: 45%;
    height: 40px;
    font-size: 12px;
    list-style: none;
    background-color: #B82E29;
    text-align: center;
    color: #FFF;
    padding: 5px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.card-footer {
    background-color: #F0D3AD;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px;
    border-radius: 5px;
    border: 2px dotted #917f686b;
}

select {
    width: 70%;
    padding: 5px;
    margin-right: 12px;
}

.delete-btn {
    background-color: #B82E29;
    border: none;
    padding: 2px;
    color: #E4E2DD;
    border-radius: 5px;
    cursor: pointer;
    transition: .5s;
}

.delete-btn:hover {
    background-color: #000;

}
</style>