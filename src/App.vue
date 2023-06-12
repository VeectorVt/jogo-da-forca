<template>
  <div id="app">
    <h1>Jogo da Forca WDEV</h1>

    <!-- Tela > Inicio>> palavra > dica > Jogo -->
    <!-- Section onde a tela é equivalente a mostrar 2 etapas -->
    <section v-if="tela === 'inicio'" id="incio">
      <!-- É Possivel importar o mesmo componente sem que ele seja igual usando props e variavéis em seus valores -->

      <Formulario
        v-if="etapa === 'palavra'"
        title="Defina a palavra"
        button="Próximo"
        :action="setPalavra"
      />

      <Formulario
        v-if="etapa === 'dica'"
        title="Defina a Dica"
        button="Iniciar jogo :)"
        :action="setDica"
      />
    </section>

    <!-- Section onde tela é equivalente a mostrar o jogo -->
    <section v-if="tela === 'jogo'" id="jogo">
      <Jogo
        :erros="erros"
        :palavra="palavra"
        :dica="dica"
        :verificarLetra="verificarLetra"
        :etapa="etapa"
        :letras="letras"
        :jogar="jogar"
        :jogarNovamente="jogarNovamente"
      />
    </section>
  </div>
</template>

<script>
import "./css/global.css";
import Formulario from "./components/Formulario";
import Jogo from "./components/Jogo";

export default {
  name: "App",
  data() {
    return {
      tela: "inicio",
      etapa: "palavra",
      palavra: "",
      dica: "",
      erros: 0,
      letras: [],
    };
  },
  components: {
    Formulario,
    Jogo,
  },

  methods: {
    setPalavra(palavra) {
      this.palavra = palavra;
      this.etapa = "dica";
    },
    setDica(dica) {
      this.dica = dica;
      this.tela = "jogo";
      this.etapa = "jogo";
    },
    verificarLetra(letra) {
      return this.letras.find(
        (item) => item.toLowerCase() === letra.toLowerCase()
      );
    },
    jogar(letra) {
      //Adiciona letra jogada
      this.letras.push(letra);

      this.verificaErros(letra);
    },
    verificaErros(letra) {
      //Acerto
      if (this.palavra.toLowerCase().indexOf(letra.toLowerCase()) >= 0) {
        return this.verificarAcertos();
      }
      //ERROS
      this.erros++;

      if (this.erros === 6) return (this.etapa = "enforcado");
    },
    verificarAcertos() {
      let letrasUnicas = [...new Set(this.palavra.split(""))];
      if (letrasUnicas.length === this.letras.length - this.erros) {
        return (this.etapa = "ganhador");
      }
    },
    jogarNovamente(){
      this.palavra = ''
      this.dica = ''
      this.erros = 0 
      this.letras = []
      this.tela = 'inicio'
      this.etapa = 'palavra'
    }
  },
};
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
