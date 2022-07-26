<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-5" role="form" aria-label="Formulário para criação de uma nova tarefa">
                <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao" />
            </div>

            <div class="column is-3">
                <div class="select">
                    <select v-model="idProjeto">
                        <option value="">Selecione o projeto</option>
                        <option :value="projeto.id" v-for="projeto in projetos" :key="projeto.id">
                            {{ projeto.name }}
                        </option>
                    </select>
                </div>
            </div>
            <div class="column">
                <Temporizador @aoTemporizadorFinalizado="finalizarTarefa"></Temporizador>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useStore } from "vuex";
import Temporizador from './Temporizador.vue'
import { key } from '@/store'
import { computed, ref } from "@vue/reactivity";
export default defineComponent({
    name: "Formulario-Component",
    emits: ['aoSalvarTarefa'],
    components: {
        Temporizador
    },

    setup(props, { emit }) {
        const store = useStore(key)
        const descricao = ref("")
        const idProjeto = ref("")
        const projetos = computed(() => store.state.projeto.projetos)

        const finalizarTarefa = (tempoDecorrido: number): void => {
            emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: descricao.value,
                projeto: projetos.value.find(proj => proj.id === idProjeto.value)
            })
            descricao.value = ''

        }

        return {
            descricao,
            idProjeto,
            projetos,
            finalizarTarefa
        }
    }
});

</script>
<style>
.formulario {
    color: var(--texto-primario);
    background-color: var(--bg-primario);
}
</style>