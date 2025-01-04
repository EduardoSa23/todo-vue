<script setup>
import { ref } from 'vue';

const props = defineProps(['tarefas']);
const emits = defineEmits(['excluirTarefa', 'editarTarefa']);

const edicaoAtiva = ref(null);
const tituloEditando = ref('');

const ativarEdicao = (index, titulo) => {
    edicaoAtiva.value = index;
    tituloEditando.value = titulo;
};

const salvarEdicao = (index) => {
    emits('editarTarefa', { index, novoTitulo: tituloEditando.value });
    edicaoAtiva.value = null;
};
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item d-flex align-items-center justify-content-between" v-for="(tarefa, index) in tarefas"
            :key="tarefa.titulo">
            <div v-if="edicaoAtiva === index" class="d-flex align-items-center flex-grow-1">
                <input v-model="tituloEditando" class="form-control me-2" type="text" />
                <button class="btn btn-success btn-sm me-2" @click="salvarEdicao(index)">
                    Salvar
                </button>
            </div>
            <div v-else class="d-flex align-items-center flex-grow-1">
                <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                    :id="tarefa.titulo" type="checkbox">
                <label :class="{ done: tarefa.finalizada }" class="ms-3 flex-grow-1" :for="tarefa.titulo">
                    {{ tarefa.titulo }}
                </label>
            </div>
            <div>
                <button class="btn btn-warning btn-sm me-2" @click="ativarEdicao(index, tarefa.titulo)">
                    Editar
                </button>
                <button class="btn btn-danger btn-sm" @click="emits('excluirTarefa', index)">
                    Excluir
                </button>
            </div>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
