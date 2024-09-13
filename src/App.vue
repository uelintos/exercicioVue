<script setup>
import { reactive } from "vue";
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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Voçê possui {{ getPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col-md-7">
        <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="Digite a tarefa">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-3">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Concluidas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getFiltradas()">
      <input @change="evento => tarefa.concluido = evento.target.checked" :checked="tarefa.concluido" :id="tarefa.titulo" type="checkbox">
      <label :class="{ done: tarefa.concluido }" class="ms-3" :for="tarefa.titulo">
        {{tarefa.titulo}}
      </label>
    </li>
  </ul>
  </div>
 
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
