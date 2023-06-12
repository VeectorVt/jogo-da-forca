<template>
  <div class="jogo">
    <Forca :erros="erros" />

    <Palavra
      :palavra="palavra"
      :dica="dica"
      :verificarLetra="verificarLetra"
      :etapa="etapa"
    />

    <Teclado
      v-if="etapa === 'jogo'"
      :jogar="jogar"
      :letras="letras"
      :verificarLetra="verificarLetra"
    />

    <Final
      :jogarNovamente="jogarNovamente"
      v-if="etapa != 'jogo'"
      :etapa="etapa"
      :texto="etapa === 'ganhador' ? 'Parabéns :)' : 'Tadinho :('"
    />
  </div>
</template>

<script>
import Forca from "./Forca";
import Teclado from "./Teclado";
import Palavra from "./Palavra";
import Final from "./Final";

export default {
  name: "Jogo",

  props: {
    erros: Number,
    palavra: String,
    dica: String,
    verificarLetra: Function,
    etapa: String,
    letras: Array,
    jogar: Function,
    jogarNovamente:Function
  },

  components: {
    Forca,
    Palavra,
    Teclado,
    Final,
  },

  data() {
    return {};
  },

  methods: {},
};
</script>

<style scoped>
.jogo {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
</style>