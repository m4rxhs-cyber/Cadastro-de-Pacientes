<template>

</template>

<script>
export default {
  name: "UF",

  mounted() {
    //Segmentação do elemento select
    let dropdown = document.getElementById("locality-dropdown");

    //Limpeza de todas as opções no elemento
    dropdown.length = 0;

    //Acrescenta a opção padrao
    let defaultOption = document.createElement("option");
    defaultOption.text = "Escolha o Estado/Distrito";

    dropdown.add(defaultOption);
    dropdown.selectedIndex = 0;

    //URL onde estão os dados JSON
    const url = "https://servicodados.ibge.gov.br/api/v1/localidades/estados";

    //Inicialização da solicitação remota
    const request = new XMLHttpRequest();
    request.open("GET", url, true);

    //Criam um elemento de opção para cada entrada encontrada e o adiciona à lista de seleção
    request.onload = function () {
      if (request.status === 200) {
        const data = JSON.parse(request.responseText);
        let option;
        for (let i = 0; i < data.length; i++) {
          option = document.createElement("option");
          option.text = data[i].nome;
          dropdown.add(option);
        }
      }
    };

    //Função para se caso houver algum erro
    request.onerror = function () {
      console.error("Um erro ocorreu ao buscar o JSON em " + url);
    };

    //Envio da solicitação remota
    request.send();
  },
};
</script>

