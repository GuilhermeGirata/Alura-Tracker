<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioHome @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <TarefaHome v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
        <BoxContainer v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </BoxContainer>
      </div>
      
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import FormularioHome from './components/Formulario.vue';
import TarefaHome from './components/Tarefa.vue';
import ITarefa from './interfaces/ITarefa';
import BoxContainer from './components/Box.vue';

export default defineComponent({
  name: 'App',

  components: {
    BarraLateral,
    FormularioHome,
    TarefaHome,
    BoxContainer
  },

  data () {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },

  computed: {
    listaEstaVazia () : boolean {
      return this.tarefas.length === 0
    }
  },

  methods: {
    salvarTarefa (tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo: boolean) {
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
  --bg-primario: #fff;
  --texto-primario: #000;
}
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}
.conteudo {
  background-color: var(--bg-primario);
}
</style>
