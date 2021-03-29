<template>
  <div class="px-64">
    <h1 class="font-mono text-6xl text-center pb-8">Pokemon List With Vue</h1>

    <div class="grid grid-cols-4 gap-8">
      <div class="shadow-md p-3 rounded-md flex flex-col	items-center " v-for="(pokemon, index) in pokemons.results" :key="index">
        <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+index+'.png'" alt="">
        {{pokemon.name}}
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';


export default {
  name: 'pokemon',
  data(){
    return{
      pokemons : []
    }
  },
   mounted () {
    axios
      .get('https://pokeapi.co/api/v2/pokemon?limit=100&offset=200')
      .then(response => (this.pokemons = response.data))
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
