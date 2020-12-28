<template>
  <div id="app">

    <h1 class="sla">Jogo da velha</h1>

    <section v-if="tela === 'inicio'" id="inicio">
      
      <Formulario 
        v-if="etapa === 'palavra'"
        title="Defina a palavra"
        button="Próximo"
        :action="setPalavra"
      />

      <Formulario 
        v-if="etapa === 'dica'"
        title="Defina a dica"
        button="Iniciar Jogo"
        :action="setDica"
      />

    </section>

    <section v-if="tela === 'jogo'" id="jogo">
      <Jogo 
        :erros="erros"
        :palavra="palavra"
        :dica="dica"
        :verificarLetra="verificarLetra"
        :etapa="etapa"
      />
    </section>

  </div>
</template>

<script>
import Formulario from './components/Formulario';
import Jogo from './components/Jogo'
import './css/global.css';

export default {
  name: 'App',
  data(){
    return {
      tela: 'inicio',
      etapa: 'palavra',
      palavra: '',
      dica: '',
      erros: 0,
      letras: ['l', 'e', 'o']
    }
  },
  components: {
    Formulario,
    Jogo
  },
  methods: {
    setPalavra: function(palavra){
      this.palavra = palavra;
      this.etapa = 'dica';
    },
    setDica: function(dica){
      this.dica = dica;
      this.tela = 'jogo';
      this.etapa = 'jogo';
    },
    verificarLetra: function(letra){
      return this.letras.find(item => item.toLowerCase() === letra.toLowerCase());
    }
  }
}
</script>

<style>
#app {
  width:100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
