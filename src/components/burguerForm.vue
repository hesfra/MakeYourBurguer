<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="burguerForm" @submit="createBurguer">
                <div class="inputContainer">
                    <label for="nome">Nome</label>
                    <input type="text" id="nome" name="nome" placeholder="Nome" v-model="nome" />
                </div>

                <div class="inputContainer">
                    <label for="pao">Escolha um pão</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}
                        </option>
                        <option value="integral">Integral</option>
                    </select>
                </div>

                <div class="inputContainer">
                    <label for="carne">Escolha a carne do seu Burguer</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}
                        </option>
                    </select>
                </div>

                <div id="OpcionaisContainer" class="inputContainer">
                    <label id="opcionaisTitle" for="opcionais">Escolha os opcionais</label>
                    <div class="checkboxContainer" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                </div>
                <input type="submit" value="Criar meu Burguer!" class="submitBtn" />
            </form>
        </div>
    </div>
</template>

<script>
import Message from './message.vue';
export default {
    name: "burguerForm",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            msg: null
        };
    },
    methods: {
        async getIgredients() {
            const req = await fetch("http://localhost:3001/ingredientes");
            const data = await req.json();
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },
        async createBurguer(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                pao: this.pao,
                carne: this.carne,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            };
            const DataJson = JSON.stringify(data);
            const req = await fetch("http://localhost:3001/burgers", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: DataJson
            });
            const res = await req.json();

            //mensagem de sistema
            this.msg = `Pedido ${res.id} realizado com sucesso!`;

            //limpar mensagem de sistema
            setTimeout(() => {
                this.msg = "";
            }, 3000);
        }
    },
    mounted() {
        this.getIgredients();
    },
    components: { Message }
}
</script>

<style scoped>
#burguerForm {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 100%;
    height: 100%;
    max-width: 400px;
    margin: 0 auto;
}

.inputContainer {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

input,
select {
    padding: 5px 10px;
    width: 300px;
}

#OpcionaisContainer {
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionaisTitle {
    width: 100%;
}

.checkboxContainer {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkboxContainer span,
.checkboxContainer input {
    width: auto;
}

.checkboxContainer span {
    margin-right: 6px;
    font-weight: bold;
}

.submitBtn {
    background-color: #222;
    color: #fcba03;
    border: 2px solid #222;
    padding: 10px;
    font-weight: bold;
    font-size: 16px;
    cursor: pointer;
    transition: 0.5s;
    
}

.submitBtn:hover {
    background-color: transparent;
    color: #222;

}
</style>