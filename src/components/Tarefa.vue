<template>
    <Box>
        <div class="columns">
            <div class="columns is-7">
                {{ tarefa.descricao || 'Tarefa sem descricao' }}
            </div>
            <div class="columns">
                <Cronometro :tempoEmSegundos="tarefa?.duracaoEmSegundos" />
            </div>
        </div>

    </Box>
</template>
<script lang="ts">
import ITarefa from "@/interfaces/ITarefa";
import { defineComponent, PropType } from "vue";
import Cronometro from './Cronometro.vue';
import Box from "./Box.vue";

export default defineComponent({
    name: 'Tarefa-Component',
    components: {
        Cronometro,
        Box
    },
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            requiered: true
        }
    }
})

</script>

