<script setup>
  import { reactive } from 'vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';
  import Cabecalho from './components/Cabecalho.vue';

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
    <Cabecalho :tarefasPendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefas-temp="estado.tarefasTemp" :edita-tarefa-temp="evento => estado.tarefasTemp = evento.target.value" :adicionar-tarefa="adicionarTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>

</template>


