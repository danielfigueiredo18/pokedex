<template>
  <div id="app">
    
    <div class="column is-half is-offset-one-quarter">
      <input class="input is-rounded" type="text" name="" id="" placeholder="Insira o nome de um Pokemon para pesquisar" v-model="busca">
      <button class="button is-fullwidth is-success" id="busca-btn" @click="buscar">Buscar</button>
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
      <Pokemom :name="poke.name" :url="poke.url" :num="index+1" />
    </div>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'
import Pokemom from './components/Pokemon'
export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
      }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res =>{
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
      console.log(this.pokemons)
    })
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca ==' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase())
      }
    }
  },
  components:{
    Pokemom
  },
  computed:{
    /*resultadoBusca: function(){
      if(this.busca == '' || this.busca ==' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }*/
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
#busca-btn{
  margin-top:2%;
}
</style>
