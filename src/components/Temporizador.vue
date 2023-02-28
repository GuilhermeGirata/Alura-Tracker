<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">  
        <CronometroHome 
            :tempoEmSegundos="tempoEmSegundos"
        />
        <BotaoHome 
            @clicado="iniciar" 
            icone="fas fa-play" 
            texto="play" 
            :desabilitado="cronometroRodando" 
        />
        <BotaoHome 
            @clicado="finalizar" 
            icone="fas fa-stop" 
            texto="stop" 
            :desabilitado="!cronometroRodando" 
        />
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronometroHome from './Cronometro.vue';
import BotaoHome from './Botao.vue';

export default defineComponent ( {
    name: 'TemporizadorHome', 

    emits: ['aoTemporizadorFinalizado'],

    components: {
        CronometroHome,
        BotaoHome
    },

    data () {
        return{
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },

    methods: {
        iniciar () {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1
            }, 1000)
        },
        finalizar () {
            this.cronometroRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>