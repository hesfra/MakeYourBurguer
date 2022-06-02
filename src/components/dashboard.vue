<template>
    <div id="burguerTable">
        <div>
            <div id="burguerTableHeading">
                <div class="orderId">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
            <div id="burguerTableRows">
                <div class="burguerTableRow" v-for="burger in burgers" :key="burger.id">
                    <div class="orderNumber">{{ burger.id }}</div>
                    <div class="clientName">{{ burger.nome }}</div>
                    <div class="pao">{{ burger.pao }}</div>
                    <div class="carne">{{ burger.carne }}</div>
                    <div class="opcionais">
                        <ul>
                            <li v-for="(opcional, index) in burger.opcionais" :key="index">
                                {{ opcional }}</li>
                        </ul>
                    </div>
                    <div>
                        <select name="status" class="status">
                          <option value="">Selecione</option>
                          <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">
                          {{ s.tipo }}
                          </option>
                        </select>
                        <button class="deleteBtn">Cancelar</button>
                    </div>
                </div>

            </div>

        </div>
    </div>
</template>

<script>
export default {
    name: "Dashboard",
    data() {
        return {
            burgers: null,
            burger_id: null,
            status: [],
        }
    },
    methods: {
        async getPedidos() {
            const req = await fetch("http://localhost:3001/burgers");
            const data = await req.json();
            this.burgers = data;

            //resgatar status
            this.getStatus();

        },
        async getStatus() {
            const req = await fetch("http://localhost:3001/status");
            const data = await req.json();
            this.status = data;
        },
    },
    mounted() {
        this.getPedidos();
    },

}
</script>

<style scoped>
#burguerTable {
    max-width: 1200px;
    margin: 0 auto;
}

#burguerTableHeading,
#burguerTableRows,
.burguerTableRow {
    display: flex;
    flex-wrap: wrap;
}

#burguerTableHeading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

#burguerTableHeading div,
.burguerTableRow div {
    width: 19%;
}

.burguerTableRow {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
}

#burguerTableHeading .orderId,
.burguerTableRow .orderNumber {
    width: 5%;
}

select {
    padding: 12px 6px;
    margin-right: 12px;
}

.deleteBtn {
    color: #fcba03;
    background-color: #222;
    padding: 10px;
    border-radius: 3px;
    cursor: pointer;
    font-weight: bold;
    border: 2px solid #222;
    font-size: 16px;
    margin: 0 auto;
    transition: 0.5s;
}

.deleteBtn:hover {
    background-color: transparent;
    color: #222;
}
</style>