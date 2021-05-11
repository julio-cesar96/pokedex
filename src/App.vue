<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon-logo.png" />
      <hr />

      <h3 class="is-size-3 titulo"> Pokédex </h3>

      <input class="input is-rounded" type="text" placeholder="Digite o nome do pokemon" v-model="busca">
      <button class="button is-rounded is-medium btn-busca" @click="buscarPokemon">Buscar Pokémon</button>

      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  components: {
    Pokemon
  },
    data() {
      return {
        pokemons: [],
        filteredPokemons: [],
        busca: ''
      }
    },
    created: function() {
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
        console.log("Os pokemons vieram");
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      })
    },
    methods: {
      buscarPokemon: function() {

        this.filteredPokemons = this.pokemons;

        if(this.busca == '' || this.busca == ' ') {
          this.filteredPokemons = this.pokemons;
        } else {
          this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
        }
      }
    },
    computed: {
      /*
      resultadoBusca: function() {
        if(this.busca == '' || this.busca == ' ') {
          return this.pokemons;
        } else {
          return this.pokemons.filter(pokemon => pokemon.name == this.busca);
        }
      }*/
    }
  }

</script>

<style>
#app {
  background-color: #ef5350;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  text-align: center;
  color: #000;
  font-weight: bold;
}

.titulo {
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-weight: bold;
  color: #fff;
}

.btn-busca {
  margin-top: 2%;
  margin-bottom: 1%;

  font-family:  'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.btn-busca:hover {
  color:#fff;
  background-color: #f38684;
}
</style>
