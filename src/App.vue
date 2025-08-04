<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefasTemp: '',
  tarefas: [
    { 
      titulo: 'Estudar Vue.js',
      concluida: false
    },
    { 
      titulo: 'Estudar JavaScript',
      concluida: true
    },
    { 
      titulo: 'Estudar HTML',
      concluida: false
    },
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.concluida);
}

const getTarefasConcluidas = () => {
  return estado.tarefas.filter(tarefa => tarefa.concluida);
}

const getTarefasFiltradas = () => { 
  const {filtro} = estado;


  switch(filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'concluídas':
      return getTarefasConcluidas();
    default:
      return estado.tarefas;
  }
}

const adicionarTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefasTemp,
    concluida: false
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefasTemp = '';
}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header> 
    <form @submit.prevent="adicionarTarefa">
    <div class="row">
      <div class="col">
        <input :value="estado.tarefasTemp" @change="evento => estado.tarefasTemp = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" />
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="estado.filtro = $event.target.value" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">pendentes</option>
          <option value="concluídas">concluídas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" :id="tarefa.titulo" type="checkbox" />
      <label :class="{ done: tarefa.concluida }" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
  </div>

</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
