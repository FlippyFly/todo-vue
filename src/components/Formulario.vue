<script setup>
const props = defineProps(['adicionarTarefa', 'tarefasTemp', 'trocarFiltro', 'editaTarefaTemp']);
</script>

<template>
        <form @submit.prevent="props.adicionarTarefa">
    <div class="row">
        <div class="col">
            <input :value="props.tarefasTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" />
        </div>
        <div class="col-md-2">
            <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
            <select @change="props.trocarFiltro" class="form-control">
                <option value="todas">Todas tarefas</option>
                <option value="pendentes">pendentes</option>
                <option value="concluídas">concluídas</option>
            </select>
        </div>
    </div>
</form>
</template>