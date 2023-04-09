<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <CronometroTracker :tempoEmSegundos="tempoEmSegundos" />
    <BotaoTemporizador
      @clicado="iniciar"
      icone="fas fa-play"
      texto="play"
      :desabilitado="cronometroRodando"
    />
    <BotaoTemporizador
      @clicado="finalizar"
      icone="fas fa-stop"
      texto="stop"
      :desabilitado="!cronometroRodando"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import CronometroTracker from '../components/CronometroTracker.vue'
import BotaoTemporizador from '../components/BotaoTemporizador.vue'

export default defineComponent({
  name: 'FormularioTracker',
  emits: ['aoTemporizadorFinalizado'],
  components: { CronometroTracker, BotaoTemporizador },
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false
    }
  },
  computed: {
    tempoDecorrido(): string {
      return new Date(this.tempoEmSegundos * 1000).toISOString().substr(11, 8)
    }
  },
  methods: {
    iniciar() {
      this.cronometroRodando = true
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1
      }, 1000)
    },
    finalizar() {
      this.cronometroRodando = false
      clearInterval(this.cronometro)
      this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
      this.tempoEmSegundos = 0
    }
  }
})
</script>
