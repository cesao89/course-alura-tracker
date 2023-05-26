<template>
    <ListaBox>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <FormularioCronometro :tempoEmSegundos="tarefa.duracaoEmSegundos" />
            </div>
        </div>
    </ListaBox>
</template>

<script lang="ts">
import {defineComponent, PropType} from 'vue'
import FormularioCronometro from './FormularioCronometro.vue';
import ITarefa from '../interfaces/ITarefa';
import ListaBox from './ListaBox.vue';

export default defineComponent({
    name: 'ListaTarefa',
    components: {
        FormularioCronometro,
        ListaBox,
    },
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
})
</script>