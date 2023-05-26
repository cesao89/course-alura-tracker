<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': this.modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioCentral @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <ListaTarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <ListaBox v-if="listaEstaVazia">
          Você não está muito produtivo hoje! :/
        </ListaBox>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import FormularioCentral from './components/FormularioCentral.vue';
import ListaTarefa from './components/ListaTarefa.vue';
import ITarefa from './interfaces/ITarefa';
import ListaBox from './components/ListaBox.vue';

export default defineComponent({
    name: "App",
    components: {
      BarraLateral,
      FormularioCentral,
      ListaTarefa,
      ListaBox
    },
    data () {
      return {
        tarefas: [] as ITarefa[],
        modoEscuroAtivo: false,
      }
    },
    computed: {
      listaEstaVazia () : boolean {
        return this.tarefas.length === 0
      }
    },
    methods: {
      salvarTarefa (tarefa : ITarefa) : void {
        this.tarefas.push(tarefa)
      },
      trocarTema (modoEscuroAtivo : boolean) : void {
        this.modoEscuroAtivo = modoEscuroAtivo
      }
    }
});
</script>

<style>
.lista {
  padding: 1.25rem;
}
main {
  --bg-primairo: #fff;
  --texto-primairo: #000;
}

main.modo-escuro {
  --bg-primairo: #2b2d42;
  --texto-primairo: #ddd;
}

.conteudo {
  background-color: var(--bg-primairo);
}
</style>
