<template>
    <FormularioHome @aoSalvarTarefa="salvarTarefa"/>
    <div class="lista">
        <TarefaHome v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
        <BoxContainer v-if="listaEstaVazia">
            Você não está muito produtivo hoje :(
        </BoxContainer>
    </div>
</template>
  
<script lang="ts">
  import { defineComponent } from 'vue';
  import FormularioHome from '../components/Formulario.vue';
  import TarefaHome from '../components/Tarefa.vue';
  import ITarefa from '../interfaces/ITarefa';
  import BoxContainer from '../components/Box.vue';
  
  export default defineComponent({
    name: 'App',
  
    components: {
      FormularioHome,
      TarefaHome,
      BoxContainer
    },
  
    data () {
      return {
        tarefas: [] as ITarefa[],
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
      }
    }
  });
</script>
  