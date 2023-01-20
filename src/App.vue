<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon-logo.png" alt="">
      <div class="div-search">
        <input class="input is-rounded" type="text" placeholder="Buscar pokemon" v-model="search">
      </div>
      <div v-for="(poke) in searchResult" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="numberPokemon(poke.url)" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon-component.vue';

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      search: '',
    }
  },
  components: {
    Pokemon
  },
  methods: {
    numberPokemon: function(url) {
      return url.match(/[^v]\d+/g)[0]?.match(/\d+/g)[0];
    }
  },
  computed: {
    searchResult: function(){
      if (this.search === '' || this.busca === ' ') {
        return this.pokemons;
      } else {
        return this.pokemons.filter(pokemon => pokemon.name.includes(this.search))
      }
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results;
    }).catch(err => {
      console.log(err);
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.div-search {
  margin: 50px 0;
}
</style>
