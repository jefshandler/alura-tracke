<template>
<main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscutoAtivo }">
  <div class="column is-one-quarter">
  <BarraLateral @aoTemaAlterado="trocarTema"/>
  </div>
  <div class="column is-three-quarter conteudo">
<Formulario @aoSalvarTarefa="salvarTarefa"/>
    <div class="lista">
      <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>

      <Box v-if="listaEstaVazia">
        Você não esta muito produtivo hoje
      </Box>
    </div>
  </div>
</main>

</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from "@/components/BarraLateral.vue";
import Formulario from "@/components/Formulario.vue";
import Tarefa from "@/components/Tarefa.vue";
import ITarefas from "@/interfaces/ITarefas";
import Box from "@/components/Box.vue";

export default defineComponent({
  name: 'App',
  components: {
    Box, BarraLateral,
      Formulario,
    // eslint-disable-next-line vue/no-unused-components
      Tarefa
  },
  data () {
    return {
      tarefas: [] as ITarefas[],
      modoEscutoAtivo: false
    }
  },
  computed: {
    listaEstaVazia () : boolean {
      return this.tarefas.length ===0
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefas) {
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivado: boolean) {
      this.modoEscutoAtivo = modoEscuroAtivado
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
