<script setup>
//Importações
import { onMounted, ref } from "vue";

//Variavel para exibir o carregamento
let carregamento = ref(true)

//Vetor contendo os Pokémons
let vetor = ref([]);

//Variavel para armazenar o termo da filtragem
let termoFiltragem = ref('')


//onMounted (Executado antes do componente ser criado, para processar informações)
//Sendo executado uma funcao assincrona para puxar os dados da API
onMounted(async () => {
  for (let indice = 1; indice <= 151; indice++) {
    let requisicao = await fetch(`https://pokeapi.co/api/v2/pokemon/${indice}`);
    let pokemon = await requisicao.json();
    vetor.value.push(pokemon);
  }

  carregamento.value = false
});


//Função para filtrar os Pokémons
function filtrar(){
  return vetor.value.filter(obj => obj.name.toLowerCase().includes(termoFiltragem.value.toLowerCase()))
}


</script>

<template>

  <div class="carregamento" v-if="carregamento">
    <img src="../complementos/carregamento.gif" alt="">
  </div>


  <main class="container" v-if="!carregamento">

    <!-- Filtragem -->
    <div class="row">
      <div class="col-12">
        <input type="text" v-model="termoFiltragem" placeholder="Qual pokemon você está procurando?" class="form-control mt-4 mb-4">

        <p v-if="filtrar().length == 0">Não foi encontrado nenhum Pokémon.</p>
        <p v-else-if="filtrar().length == 1">Foi encontrado apenas um Pokémon.</p>
        <p v-else>Foram encontrados {{filtrar().length}} Pokémons.</p>
      </div>
    </div>

    <!-- Listagem -->
    <div class="row">

      <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="(v, index) in filtrar()" :key="index">

        <div class="card" :class="v.types[0].type.name">
          <img :src="v.sprites.other.dream_world.front_default">
          <p>{{v.name}}</p>
        </div>
        
      </div>

    </div>
  </main>
</template>
