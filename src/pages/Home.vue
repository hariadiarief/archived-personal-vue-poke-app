<template>
  <div class="px-5 md:px-32 pb-64">
    <h1 class="font-mono text-6xl text-center pb-8">Pokemon List With Vue</h1>

    <div class="grid grid-cols-2 md:grid-cols-4 gap-8">
      <router-link
        class="shadow p-3 rounded-md flex flex-col items-center hover:shadow-md"
        :to="'/detail/' + pokemon.name"
        v-for="(pokemon, index) in pokemons"
        :key="index"
      >
        <img
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
            index + 1
          }.png`"
          :alt="pokemon.name"
        />
        {{ pokemon.name }}
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      pokemons: [],
      limit: 25,
      offset: 0,
      isNext: null,
    };
  },
  methods: {
    getPokemon() {
      axios
        .get(
          `https://pokeapi.co/api/v2/pokemon?limit=${this.limit}&offset=${this.offset}`
        )
        .then((response) => {
          this.pokemons = this.pokemons.concat(response.data.results);
          this.isNext = response.data.next;
        });
    },
    nextPage() {
      window.onscroll = () => {
        let bottomOfWindow =
          document.documentElement.scrollTop + window.innerHeight ===
          document.documentElement.offsetHeight;
        if (bottomOfWindow) {
          this.offset += this.offset;
          this.getPokemon();
        }
      };
    },
  },
  beforeMount() {
    this.getPokemon();
  },
  mounted() {
    this.nextPage();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
