<script setup>
import { reactive } from "vue";
import Formulario from "./components/Formulario.vue";
import Cabecalho from "./components/Cabecalho.vue";
import Lista from "./components/Lista.vue";

const estado = reactive({ 
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar Java',
      concluido: false,
    },
    {
      titulo: 'Estudar PHP',
      concluido: true,
    },
    {
      titulo: 'Estudar React',
      concluido: false,
    }
  ]
})

const getPendentes = () => { 
  return estado.tarefas.filter(tarefa => !tarefa.concluido) 
}
const getConcluidas = () => {
  return estado.tarefas.filter(tarefa => tarefa.concluido)
}

const getFiltradas = () => {
  const { filtro } = estado;

  switch (filtro){
    case 'pendentes': 
      return getPendentes()
    case 'finalizadas': 
      return getConcluidas()
    default:
      return estado.tarefas
  }
}

const cadastraTarefa = () =>{
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    concluido: false
  }
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = ''
}

</script>

<template>

  <div class="container">
    <Cabecalho :tarefas-pendentes="getPendentes().length" />
    <Formulario :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" :edita-filtro="evento => estado.filtro = evento.target.value" />
    <Lista :tarefas="getFiltradas()" :tarefas-pendentes="getPendentes().length"/>
  </div>
 
</template> 
