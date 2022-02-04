<template>
  <div class="main-container">
    <h1>Cadastro dos Pacientes</h1>
    <CadastroForm />
  </div>
</template>

<script>
import CadastroForm from '../components/CadastroForm.vue';

export default {
  name: "Home",
  components: {
    CadastroForm
  }
}
</script>
