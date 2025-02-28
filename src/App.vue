
<template>
  <div class="container">
    <Cabecalho :tarefasPendentes="getTarefasPendentes().length" />
    <Formulario @nova-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>

<script setup>
import { reactive } from 'vue';
import Cabecalho from '@/components/Cabecalho.vue';

import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    { titulo: 'Estudar ES6', finalizada: false },
    { titulo: 'Estudar Sass', finalizada: false },
    { titulo: 'Ir para a academia', finalizada: true },
  ],
});

const getTarefasPendentes = () => estado.tarefas.filter(tarefa => !tarefa.finalizada);

const getTarefasFinalizadas = () => estado.tarefas.filter(tarefa => tarefa.finalizada);

const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
};

const cadastraTarefa = (novaTarefa) => {
  const tarefaNova = {
    titulo: novaTarefa,
    finalizada: false,
  };
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
};
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
