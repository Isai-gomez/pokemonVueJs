<template>
  <h1 v-if="!pokemon">Cargando....</h1>
  <div v-else>
    <h2>
      ¿Quien es este Pokemon?
    </h2>
    <!-- TODO Picture -->
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />

    <!-- TODO Option -->
    <PokemonOption :optiones="pokemonArray" />
  </div>
</template>
<script>
import PokemonPicture from '../components/PokemonPicture.vue'
import PokemonOption from '../components/PokemonOption.vue'
import getPokemonOption from '../helper/getPokemonOption'
// console.table(getPokemonOption().then((data) => data))
export default {
  components: {
    PokemonPicture,
    PokemonOption,
  },
  data() {
    return { pokemonArray: [], pokemon: null, showPokemon: true }
  },
  methods: {
    async getDataPokemon() {
      this.pokemonArray = await getPokemonOption()
      const randomPokemon = Math.floor(Math.random() * 4)
      console.log(randomPokemon)
      this.pokemon = this.pokemonArray[randomPokemon]
    },
  },
  mounted() {
    this.getDataPokemon()
  },
}
</script>
