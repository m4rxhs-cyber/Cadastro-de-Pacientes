<template>
  <div>
     <Message :msg="msg" v-show="msg"/>
    <div class="box">
      
      <form method="POST" @submit="createPaciente">
        
        <fieldset>
          <legend><b> Cadastro</b></legend>
          <br />

          <div class="input-container">
            <label for="nome">Nome do cliente:</label>
            <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome"/>
          </div>
          

          <div class="input-container">
            <label for="cpf">CPF:</label>
            <input type="text" id="cpf" name="cpf" v-model="cpf" placeholder="Digite o seu CPF"/>
          </div>
          
         
         <div class="input-container">
          <label for="data_nascimento"><b> Data de Nascimento:</b></label>
          <input type="date" name="data_nascimento" id="data_nascimento" v-model="data_nasc"/>
          
          </div> 

          <div class="input-container">
            <label for="peso">Peso:</label>
            <input type="text" id="peso" name="peso" v-model="peso" placeholder="Digite o seu peso"/>
          </div>
          

          <div class="input-container">
            <label for="altura">Altura:</label>
            <input type="text" id="altura" name="altura" v-model="altura" placeholder="Digite a sua altura"/>
          </div>
          

          <h3>Escolha o Estado/Distrito:</h3>
          

          <div class="input-container">
          <select id="locality-dropdown" name="locality" v-model="uf" required>
            <UF />
          </select>
          </div>
          <br />

          <div class="input-container">
              <input type="submit" class="submit-btn" id="submit" value="Cadastrar Paciente">
          </div>

        </fieldset>
      </form>
    </div>
  </div>
</template>

<script>
import UF from "./UF.vue";
import Message from "./Message.vue";

export default {
  name: "CadastroForm",
  data() {
    return {
        nome: null,
        cpf: null,
        data_nasc: null,
        peso: null,
        altura: null,
        uf: "Escolha o Estado/Distrito",
        msg: null
    }  
  },
  methods: {
     async createPaciente(e) {
        
        e.preventDefault();

        const data = {
            nome: this.nome,
            cpf: this.cpf,
            data_nasc: this.data_nasc,
            peso: this.peso,
            altura: this.altura,
            uf: this.uf
        }

        const dataJson = JSON.stringify(data);

        const req = await fetch("https://cadastro-pacientes.herokuapp.com/Dados_Pacientes", {
            method: "POST",
            headers: {"Content-Type": "application/json"},
            body: dataJson
        });

        const res = await req.json();

        //colocar uma msg de sistema
        this.msg = `Paciente ${res.nome} cadastrado com sucesso`;
        
        //limpar msg
        setTimeout(() => this.msg = "", 3000)

        //limpar os campos
        this.nome= "";
        this.cpf= "";
        this.data_nasc= "";
        this.peso= "";
        this.altura= "";
        this.uf= "Escolha o Estado/Distrito";
     } 
  },
  components: {
    UF,
    Message
    
  },
};
</script>

<style scoped>
.box {
  color: white;  
  margin: 0 auto;
  background-image: linear-gradient(to right,rgb(194, 47, 88),rgb(194, 17, 67));
  padding: 10px;
  border-radius: 15px;
  max-width: 400px;
}

fieldset {
  border: 3px solid #222;
}

legend {
  border: 1px solid rgb(199, 10, 54);
  padding: 10px;
  text-align: center;
  background-color: #222;
  border-radius: 8px;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin: 0px 9px 4px 4px;
}

input, select {
    padding: 5px 10px;        
    letter-spacing: 3px;
    font-size: 17px;
    margin: 10px 10px;
    border-radius: 20px;
    border: none;
    outline: none;
}



label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #FFF;
    
}

h3 {
  font-size: 15px;
  margin: 10px 10px;
}

#data_nascimento {
  border: none;
  outline: none;
  padding: 4px;
  margin-left: 3px;
  margin-right: 5px;
  border-radius: 10px;
  font-size: 15px;
  
}

#locality-dropdown {
  width: auto;
  font-size: 15px;
  border: none;
  outline: none;
  padding: 6px;
  border-radius: 15px;
  text-align: center;
}

#submit{
    background-color: #222;
    color: #FFF;
    width: 330px;
    border-radius: 15px;
    border: none;
    padding: 15px;
    font-size: 14px;
    cursor: pointer;
}

#submit:hover{
    background-color: rgb(167, 26, 57);
}
</style>

