<script setup>

const props = defineProps(['tarefas', 'tarefasPendentes'])
</script>
<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-if="props.tarefasPendentes > 0" v-for="tarefa in props.tarefas">
        <input @change="evento => tarefa.concluido = evento.target.checked" :checked="tarefa.concluido" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.concluido }" class="ms-3" :for="tarefa.titulo">
            {{tarefa.titulo}}
        </label>
        </li>
        <h3 v-else class="message__done text-center fw-bold pt-5">Voçê concluiu todas as suas tarefas, Parabéns!</h3>
    </ul>
</template>
<style scoped>
  .done{
    text-decoration: line-through;
  }
  .message__done{
    transition: opacity 0.5s ease;
  }
</style>