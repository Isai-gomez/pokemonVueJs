<template>
  <h1 v-if="!pokemon">Cargando....</h1>
  <div class="wrapper-game" v-else>
    <h2>
      ¿Qué pokemon soy?
    </h2>
    <hr />
    <!-- TODO Picture -->
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />

    <!-- TODO Option -->
    <PokemonOption
      v-if="showOption"
      :optiones="pokemonArray"
      @selectionOption="selectionActive($event)"
    />

    <div class="hidden-pokemon message" v-if="showPokemon">
      <h2>{{ message }}</h2>
      <button @click="newGame" class="btn-game">New Game</button>
    </div>
  </div>
</template>
<script>
import PokemonPicture from '../components/PokemonPicture.vue'
import PokemonOption from '../components/PokemonOption.vue'
import getPokemonOption from '../helper/getPokemonOption'
export default {
  components: {
    PokemonPicture,
    PokemonOption,
  },
  data() {
    return {
      pokemonArray: [],
      pokemon: null,
      showPokemon: false,
      message: '',
      showOption: true,
    }
  },
  methods: {
    async getDataPokemon() {
      this.pokemonArray = await getPokemonOption()
      const randomPokemon = Math.floor(Math.random() * 4)
      this.pokemon = this.pokemonArray[randomPokemon]
    },
    selectionActive(idPokemon) {
      this.showPokemon = true
      if (this.pokemon.id == idPokemon) {
        this.message = `Exelente es ${this.pokemon.name.toUpperCase()}`
      } else {
        this.message = `Menso(a) es ${this.pokemon.name.toUpperCase()}`
      }
      this.showOption = false
    },
    newGame() {
      ;(this.pokemonArray = []),
        (this.pokemon = null),
        (this.showPokemon = false),
        (this.message = ''),
        (this.showOption = true),
        this.getDataPokemon()
    },
  },
  mounted() {
    this.getDataPokemon()
  },
}
</script>
<style lang="css" scope>
.message {
  padding: 0.5rem;
}
.wrapper-game {
  width: 50%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  background-color: rgba(0, 0, 0, 0.281);
  margin-left: auto;
  margin-right: auto;
  box-sizing: content-box;
  overflow: hidden;
}
.btn-game {
  background-color: #15861e;
  border: none;
  width: 10rem;
  height: 2rem;
  color: white;
}
h2 {
  color: white;
}
hr {
  width: 100%;
  height: 4px;
  border: none;
  background-color: #333;
}
@media (max-width: 700px) {
  .wrapper-game {
    width: 95%;
  }
}
</style>
