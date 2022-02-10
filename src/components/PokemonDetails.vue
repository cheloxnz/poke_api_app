<template>
  <div class="detail">
    <div class="detail-view" v-if="show">

      <div v-if="pokemon" class="image">
        <img :src="imageUrl + pokemon.id + '.png'" alt="">
      </div>

      <div v-if="pokemon" class="data">

        <h2>{{ pokemon.name }}</h2>
        <h5>Peso: {{ pokemon.weight / 10 }} Kg </h5>

        <div class="property stats" v-if="pokemon">
            <h3>Estadísticas</h3>
                <div
                    class="info-name"
                    v-for="(value, index) in pokemon.stats"
                    :key="'value'+index">
                    {{ value.stat.name }}

                </div>

                <div
                    class="info-value"
                    v-for="(value1, index1) in pokemon.stats"
                    :key="'value1'+index1">
                    {{ value1.base_stat }}
                </div>
        </div>

        <div class="property" v-if="pokemon">
          <h3>Habilidades</h3>
            <div class="abilities">
                <div class="ability" 
                    v-for="(value2, index2) in pokemon.abilities"
                    :key="'value2'+index2">
                    {{ value2.ability.name }}
                </div>
            </div>
        </div>

        <div class="property" v-if="pokemon">
            <h3>Lista de Movimientos</h3>
            <select v-model="test">
                <option 
                    v-for="(value3, index3) in pokemon.moves"
                    :key="'value3'+index3">
                    {{ value3.move.name }}
                    </option>
            </select>

            <div class="types">
          <div class="type" 
            v-for="(value4, index4) in pokemon.types"
            :key="'value4'+index4">
            {{ value4.type.name }}
          </div>
      </div>
        </div>        
      </div>
      <h2 v-else>The pokemon was not found</h2>
      <button class="close" @click="closeDetail()">
        <span class="material-icons">
          close
        </span>
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    props: [
      'pokemonUrl',
      'imageUrl'
    ],
    data: () => {
      return {
        show: false,
        pokemon: {},
        test: null,
      }      
    },
    methods: {
      fetchData() {
        let req = new Request(this.pokemonUrl);
        fetch(req)
          .then((resp) => {
            if(resp.status === 200)
              return resp.json();
          })
          .then((data) => {
              console.log(data);
            this.pokemon = data;
            this.show = true;
          })
          .catch((error) => {
            console.log(error);
          })
      },
      closeDetail() {
        this.$emit('closeDetail');
      }
    },
    created() {
      this.fetchData();
    },
  }
</script>

<style scoped>
  .detail {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    position: fixed;
    top: -16px;
    left: 0;
    margin-bottom: 100px;
    padding: 5em 1rem  1rem;
    width: calc(100% - 20px);
    height: calc(100vh - 20px);
    background-color: transparent;
  }
    .detail-view {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      position: relative;
      width: 100%;
      max-width: 510px;
      padding: 6px 0 0;
      background-color: #e2e2e2;
      border-radius: 5px;
      box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);
    
    }
      .image {
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        top: -60px;
        width: 84px;
        height: 84px;
        background: #f12711;
        background: -webkit-linear-gradient(to left, #f8aa00, #f12711);
        background: linear-gradient(to left, #ffae00, #f12711);
        border-radius: 50%;
        overflow: hidden;
        box-shadow: 0 15px 30px rgba(0,0,0,.2),
                    0 10px 10px rgba(0,0,0,.2);
      }
      h2 {
        text-transform: capitalize;
      }
      .data {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        flex-direction: column;
        width: 100%;
      }
        .property {
          width: 90%;
          max-width: 400px;
          border-bottom: 1px solid #ccc;
          margin-bottom: 10px;
          float: left;
          float: right;
        }
        h3 {
          width: 90%;
          max-width: 400px;
          border-bottom: 1px solid #ccc;
        }
        .types, .abilities {
          display: flex;
          justify-content: flex-start;
          flex-wrap: wrap;
          width: 90%;
          max-width: 400px;
        }
         .type, .ability {
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
          .type { background-color: #0A2E50; }
          .ability { background-color: #1100fc; }
      .close {
        outline: none;
        border: none;
        border-radius: 50px;
        background-color: #333;
        color: #efefef;
        padding: 10px 20px;
        margin-bottom: 20px;
        font-size: 1.2rem;
        cursor: pointer;
      }

      .close:hover{
          color: rgb(12, 63, 63);
          background-color: #b3b4b6;
          box-shadow: 0 7px 7px rgba(0,0,0,.2),
                  0 5px 5px rgba(0,0,0,.2);
        }
    i {
      font-size: 2rem;
      color: #efefef;
    }

    .info-name {
        position: relative;
        top: 0;
        right: 150px;
    }

    .info-value {
        position: relative;
        bottom: 125px;
        left: 150px;
    }

    .stats {
        height: 220px;
    }
</style>