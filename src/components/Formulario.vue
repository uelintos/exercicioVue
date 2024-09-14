<script setup>
const props = defineProps(['tarefaTemp', 'cadastraTarefa', 'editaTarefaTemp', 'editaFiltro'])
</script>
<template>
<form @submit.prevent="props.cadastraTarefa">
    <div class="row">
        <div class="col-md-7">
            <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" class="form-control" placeholder="Digite a tarefa">
        </div>
        <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-3">
            <select @change="props.editaFiltro" class="form-control">
                <option value="todas">Todas tarefas</option>
                <option value="pendentes">Pendentes</option>
                <option value="finalizadas">Concluidas</option>
            </select>
        </div>
    </div>
</form>
</template>