<script setup>
const props = defineProps(['tarefas']);
const emits = defineEmits(['excluirTarefa']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item d-flex align-items-center justify-content-between" v-for="(tarefa, index) in tarefas"
            :key="tarefa.titulo">
            <div>
                <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                    :id="tarefa.titulo" type="checkbox">
                <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                    {{ tarefa.titulo }}
                </label>
            </div>
            <button class="btn btn-danger btn-sm" @click="emits('excluirTarefa', index)">
                Excluir
            </button>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
