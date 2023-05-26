<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulário para criação de uma nova tarefa">
                <input 
                    type="text"
                    class="input"
                    placeholder="Qual tarefa você deseja criar?"
                    v-model="descricao"
                />
            </div>
            <div class="column">
                <FormularioTemporizador @aoTemporizadorFinalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import FormularioTemporizador from './FormularioTemporizador.vue';
export default defineComponent({
    name: "FormularioCentral",
    emits: ['aoSalvarTarefa'],
    components: {
        FormularioTemporizador
    },
    data () {
        return {
            descricao: ''
        }
    },
    methods: {
        finalizarTarefa (tempoDecorridos : number) : void {
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorridos,
                descricao: this.descricao
            })
            this.descricao = ''
        }
    }
})
</script>

<style>
.formulario {
    color: var(--texto-primairo);
    background-color: var(--bg-primairo);
}
</style>