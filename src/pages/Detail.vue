<template>
  <div class="px-64" v-if="pokemon">
    <h1 class="font-mono text-6xl text-center pb-8">{{ pokemon.name }}</h1>
    <img :src="pokemon.sprites.front_default" alt="" />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Detail",
  data() {
    return {
      pokemon: null,
    };
  },
  beforeMount() {
    axios
      .get(`https://pokeapi.co/api/v2/pokemon/${this.$route.params.id}`)
      .then((response) => (this.pokemon = response.data));
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
