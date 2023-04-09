<template>
  <BoxTracker>
    <div class="columns">
      <div class="column is-7">{{ tarefa.descricao || 'Tarefa sem descrição' }}</div>
      <div class="column">
        <CronometroTracker :tempoEmSegundos="tarefa.duracaoEmSegundos" />
      </div>
    </div>
  </BoxTracker>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import type { PropType } from 'vue'
import CronometroTracker from './CronometroTracker.vue'
import type ITarefa from '@/interfaces/ITarefa'
import BoxTracker from './BoxTracker.vue'

export default defineComponent({
  name: 'ListaTarefas',
  components: { CronometroTracker, BoxTracker },
  props: {
    tarefa: {
      type: Object as PropType<ITarefa>,
      required: true
    }
  }
})
</script>
