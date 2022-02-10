<template>
  <div class="container">
    <div class="title-pokemon">
      <img src="../assets/pokemon-23.svg" width="300" alt="Logo Pokemon"> <br/>
      <img src="../assets/pokedex.svg" width="250" alt="Logo Pokedex">

      <PokemonList 
        :imageUrl="imageUrl"
        :apiUrl="apiUrl"
        @setPokemonUrl="setPokemonUrl"
      />

      <PokemonDetails 
        v-if="showDetail"
        :pokemonUrl="pokemonUrl"
        :imageUrl="imageUrl"
        @closeDetail="closeDetail"
      />
    </div>
  </div>
</template>

<script>
import PokemonList from './PokemonList.vue';
import PokemonDetails from './PokemonDetails.vue';

export default {
  name: 'Pokemon',
  components: {
    PokemonList,
    PokemonDetails,
  },
  props: {
    msg: String
  },

  data: () => {
    return {
      imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
      apiUrl: 'https://pokeapi.co/api/v2/pokemon?limit=24&offset=24',
      pokemonUrl: '',
      showDetail: false,
    }
  },

  methods: {
    setPokemonUrl(url) {
      this.pokemonUrl = url;
      this.showDetail = true;
    },
    closeDetail() {
      this.pokemonUrl = '';
      this.showDetail = false;
    },
  },
}
</script>


<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Mali:wght@300&family=Manrope:wght@300&display=swap');

  .title-pokemon {
    position: absolute;
    top: 10px;
  }

  .container {
    position: absolute;
    top: 0px;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 99.8vw;
    height: 100vh !important;
    background: #f12711;
    background: -webkit-linear-gradient(to right, #f5af19, #f12711);
    background: linear-gradient(to right, #f5af19, #f12711);
    font-family: 'Mali', cursive;
    font-size: 1rem;
    margin-bottom: 100px;
    font-weight: normal;
    
  }

</style>
