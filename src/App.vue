<script setup>
//Importação dos elementos vue-router
import { RouterLink, RouterView } from "vue-router";

//Importação do Bootstrap (é instalado direto no APP, pois assim ja pega em todos os componentes)
import "bootstrap/dist/css/bootstrap.min.css";

//Importar estilo CSS
import './complementos/estilos.css'

//Importar componente de navegação
import BarraNavegacao from "./componentes/BarraNavegacao.vue";
</script>

<template>
  <!-- Barra de navegação -->
  <BarraNavegacao />

  <!-- Visualizar conteúdo das páginas -->
  <RouterView />
</template>
