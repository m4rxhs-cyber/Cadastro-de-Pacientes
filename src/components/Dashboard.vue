<template>
    <div id="pacientes-table">
        <Message :msg="msg" v-show="msg"/>
        <div>
            <div id="pacientes-table-heading">
                <div class="paciente-id">#</div>
                <div>Paciente:</div>
                <div>CPF:</div>
                <div>Data de Nascimento:</div>
                <div>Peso:</div>
                <div>Altura:</div>
                <div>UF:</div>
                <div>Ações</div>
            </div>
            <div id="pacientes-tables-rows">
                <div class="paciente-table-row" v-for="Dado in Dados_Pacientes" :key="Dado.id">
                    <div class="paciente-number">{{ Dado.id }}</div>
                    <div>{{ Dado.nome }}</div>
                    <div>{{ Dado.cpf }} </div>
                    <div>{{ Dado.data_nasc }}</div>
                    <div>{{ Dado.peso }}</div>
                    <div>{{ Dado.altura }}</div>
                    <div>{{ Dado.uf }}</div>
                    <button class="delete-btn" @click="deletePaciente(Dado.id)">Remover Paciente</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Message from "./Message.vue";

export default {
    name: 'Dashboard',
    data() {
        return {
            Dados_Pacientes: null,
            paciente_id: null,
            msg: null
        }
    },
    methods: {
        async getPacientes() {

            const req = await fetch("https://cadastro-pacientes.herokuapp.com/Dados_Pacientes");

            const data = await req.json();

            this.Dados_Pacientes = data;

            
            
        },
        async deletePaciente(id) {

            const req =  await fetch(`https://cadastro-pacientes.herokuapp.com/Dados_Pacientes/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            // msg
            this.msg = `Paciente removido com sucesso!`;
        
            //limpar msg
            setTimeout(() => this.msg = "", 3000)

            this.getPacientes();

        }
    },
    mounted() {
        this.getPacientes();
    },
    components: {
        Message
    }
}
</script>

<style scoped>

#pacientes-table {
    max-width: 1400px;
    margin: 0 auto;
}

#pacientes-table-heading,
#pacientes-table-rows,
.paciente-table-row {
    display: flex;
    flex-wrap: wrap;
}

#pacientes-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #222;
}

#pacientes-table-heading div,
.paciente-table-row div {
    width: 12%;
}

.paciente-table-row {
    width: 100%;
    padding: 10px;
    border-bottom: 1px solid #CCC;
    
}

#pacientes-table-heading .paciente-id,
.paciente-table-row .paciente-number {
    width: 8%;
}

.delete-btn{
    background-color: #222;
    color: #FFF;
    font-weight: bold;
    border: 2px solid #222;
    padding: 16px;
    cursor: pointer;
    transition: .5s;
    border-radius:20px ;
}

.delete-btn:hover{
    background-color: rgb(167, 26, 57);
}
</style>