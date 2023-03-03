<template>
  <section class="is-flex is-align-items-center is-justify-content-space-between">
    <CronometroTarefa :tempoEmSegundos="tempoEmSegundos"/>
    <BotaoTarefa @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroRodando" />
    <BotaoTarefa @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroRodando" />
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import BotaoTarefa from './BotaoTarefa.vue'
import CronometroTarefa from './CronometroTarefa.vue'


export default defineComponent({
    name: 'TemporizadorTarefa',
    emits:['aoTemporarizadorFinalizado'],
    components: {
      CronometroTarefa,
      BotaoTarefa
    },
    data () {
      return {
        tempoEmSegundos:0,
        cronometroTarefa: 0,
        cronometroRodando: false
        
      }
    },
    methods: {
      iniciar(){
        this.cronometroRodando = true
        this.cronometroTarefa = setInterval(() => {
         this.tempoEmSegundos += 1
        }, 1000)
      },
      finalizar(){
        this.cronometroRodando = false;
        clearInterval(this.cronometroTarefa);
        this.$emit('aoTemporarizadorFinalizado', this.tempoEmSegundos);
        this.tempoEmSegundos = 0
      }
    }
})
</script>
