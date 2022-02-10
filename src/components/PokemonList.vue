<template>
  <div class="list">
    <article v-for="(pokemon, index) in pokemons"
    :key="'poke'+index"
    @click="setPokemonUrl(pokemon.url)">
      <h3 style="margin-top: 10px">{{ pokemon.name }}</h3>
      <img :src="imageUrl + pokemon.id + '.png'" width="96" height="96" alt="">
    </article>
  </div>
</template>

<script>
  export default {
    props: [
      'imageUrl',
      'apiUrl',
      'pokemonUrl',
    ],
    data: () => {
      return {
        pokemons: [],
        nextUrl: '',
        pokemone: {},
        currentUrl: '',
      }
    },

    methods: {
       fetchData() {
        let req = new Request(this.currentUrl);
        fetch(req)
          .then((resp) => {
            if(resp.status === 200)
              return resp.json();
          })
          .then((data) => {
            this.nextUrl = data.next;
            data.results.forEach(pokemon => {
              pokemon.id = pokemon.url.split('/')
                .filter(function(part) { return !!part }).pop();
              this.pokemons.push(pokemon);
            });
          })
          .catch((error) => {
            console.log(error);
          })
      },
      next() {
        this.currentUrl = this.nextUrl;
        this.fetchData();
      },
      setPokemonUrl(url) {
        this.$emit('setPokemonUrl', url);
      },

    },
    created() {
      this.currentUrl = this.apiUrl;
      this.fetchData();
    },
    mounted() {

    }
  }
</script>

<style scoped>

  .list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    grid-gap: 10px;
    width: 100%;
    max-width: 1000px;
  }

    article {
      height: 130px;
      background: #659999;  /* fallback for old browsers */
      background: -webkit-linear-gradient(to right, #f4791f, #659999);  /* Chrome 10-25, Safari 5.1-6 */
      background: linear-gradient(to right, #f4791f, #659999); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
      text-align: center;
      text-transform: capitalize;
      border-radius: 5px;
      cursor: pointer;
      transition: all 1s ease;
      box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);
    }

    article:hover{
        background-color: #d7e6ec81;
    }

    h3 {
     margin: 0;
    }

    .types {
      display: flex;
      justify-content: flex-start;
      flex-wrap: wrap;
      width: 90%;
      max-width: 400px;
    }

    .type {
      margin: 0 10px 10px 0;
      padding:.5em .4em;
      border-radius: 10px;
      color: #fff;
      font-size: .8em;
      letter-spacing: 2px;
      text-transform: capitalize;
      word-wrap: none;
      word-break: keep-all;
    }
    
    .type { 
      background-color: #0A2E50; 
    }
    
    .button-add {
      position: relative;
      top: 25px;
      right: 51px;
    }
</style>