<template>
  <div id="app">
    <br/>
    <img src="./assets/logo.png">
    <br/>
    <h4 class="is-size-3">Pokedex</h4>
      <div class="column is-half is-offset-one-quarter">
        <input id="busca" type="text" class="input is-rounded" placeholder="Buscar pokemon pelo nome" v-model="busca">
        <button id="buscaBtn" class="button is-fullwidth is-fullwidth is-warning" @click="buscar">Buscar</button>
      </div>
      
      <div class="columns is-multiline is-mobile">
        
          <div id="card" class="column is-one-third is-narrow" v-for="(poke, index) in filteredPokemons" :key="poke.url">
            <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
          </div>
        
      </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';


export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: '',
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Lista de Pokemons"); 
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
      })
  },

  components: {
    Pokemon,
  },

    methods: {
    buscar: function() {
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
       this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase());
      }
    }
  },
  }

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color:#3b2e5a;
  text-align: center;
  margin-top: 0px;
  color: #e8e9b6;
  padding: 1%;
}
#buscaBtn {
  margin-top: 1%;
  margin-bottom: 2%;
}

</style>