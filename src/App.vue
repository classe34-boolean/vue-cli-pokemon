<template>
  <div id="app">
    <Header title="I pokemon di classe #34" />

    <main>
      <CustomForm 
        inputPlaceholder="Scrivi qui il nome del pokemon che vuoi cercare"
        @sendForm="searchPokemon" />

      <CustomForm 
        inputPlaceholder="Scrivi qui la tipologia di pokemon"
        @sendForm="searchType" />  
      
      <Cards :items="pokemons" />
    </main>
  </div>
</template>

<script>
import axios from 'axios';

import Header from './components/Header';
import Cards from './components/Cards';
import CustomForm from './components/CustomForm';

export default {
  name: 'App',
  components: {
    Header,
    Cards,
    CustomForm
  },
  data() {
    return {
      base_url: "https://pokeapi.co/api/v2/",
      pokemons: []
    }
  },
  methods: {
    searchPokemon: function(text) {
      axios
        .get(`${this.base_url}pokemon/${text}`)
        .then(
          res => {
            console.log(res.data);
            this.pokemons = [
              {
                name: res.data.name,
                url: `${this.base_url}pokemon/${text}`,
                img: res.data.sprites.other.dream_world.front_default
              }
            ];
          }
        )
        .catch(
          err => {
            console.log(err);
            this.pokemons = [];
          }
        );
    },
    searchType: function(text) {
     axios
      .get(`${this.base_url}type/${text}`)
      .then(
        (res) => {
          console.log(res.data.pokemon);

          this.pokemons = res.data.pokemon.map(
            (element) => {

              const urlArray = element.pokemon.url.split("/");
              const pokemonId = urlArray[urlArray.length - 2];
              // https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/132.svg
              const imgPath = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${pokemonId}.svg`;

              return {
                ...element.pokemon,
                img: imgPath
              };
            }
          );
        }
      )
      .catch(
        (err) => {
          console.log(err);
        }
      );
    }
  },
  created() {
    axios
      .get(`${this.base_url}pokemon`)
      .then(
        (res) => {
          // this.pokemons = res.data.results;

          // this.pokemons.forEach(
          //   (element) => {
          //     const urlArray = element.url.split("/");
          //     const pokemonId = urlArray[urlArray.length - 2];
          //     console.log(pokemonId);
          //   }
          // );

          this.pokemons = res.data.results.map(
            (element) => {
              const urlArray = element.url.split("/");
              const pokemonId = urlArray[urlArray.length - 2];
              // https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/132.svg
              const imgPath = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${pokemonId}.svg`;
              
              return {
                ...element,
                img: imgPath
              };

            }
          );
        }
      )
      .catch(
        (err) => {
          console.log(err);
        }
      );
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

main {
  width: 80%;
  margin: 30px auto;
}
</style>
