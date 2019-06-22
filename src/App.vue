<template>
  <v-app>

      <div id="wrapping-div">
        <div class="divSeePokemons" v-if="showDivPokemon">
          <ListPokemons  :infoPokemonsProp="infoPokemons" :imagesPokemonsProp="imagesPokemons"/>
        </div>

        <div class="divSinglePokemon" v-if="showDivSinglePokemon">
          <SinglePokemon :infoSinglePokemonProp="infoPokemons" />
        </div>
      </div>

      <v-layout>
        <v-flex xs12 sm6 offset-sm3>
          <v-card>
            <v-img
            :src="images.mainImg" class="img">
             </v-img>

            <v-card-title primary-title>
              <div>
                <h3 class="headline mb-0">Welcome to Pokemons' App</h3>
                
              </div>
            </v-card-title>

            <v-card-actions>
              <v-btn flat class="purple accent-1" @click="showPokemons(), listPokemonsImages(), countPokemonsNames()" >get Pokemons</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
  </v-layout>

      
  </v-app>
</template>

<script>
import SinglePokemon from "./SinglePokemon.vue"
import ListPokemons from "./ListPokemons.vue"


  export default {

    name: 'App',
     components: {
      ListPokemons,
      SinglePokemon
    },
   
    data () {
      return {
        infoPokemons: "pokemons",
        imagesPokemons: "images",
        showDivPokemon: false,
        showDivSinglePokemon: false,
        images: {
          mainImg: require('./assets/img/pokemons.jpg'),
        },
    
      }
    },

    methods: {
      getPokemons() {
        console.log("Hello, I work!");
        const axios = require('axios');
        axios.get('https://pokeapi.co/api/v2/pokemon/')
        .then(response => (this.infoPokemons = response.data.results))
        .catch(function (error) {
        console.log("THIS IS THE ERROR:",error);
        })
        return this.infoPokemons
      },

      getPokemonsImages() {
        console.log("Hello, I workkkkkkk!");
        const axios = require('axios');
        axios.get('https://pokeapi.co/api/v2/pokemon-form/1/')
        .then(response => (this.imagesPokemons = response.data.sprites.front_default))
        .catch(function (error) {
        console.log("THIS IS THE ERROR:",error);
        })
        return this.imagesPokemons
      },

      showPokemons() {
        this.toggleClass();
        this.toggleClassSinglePokemon()
      },

      toggleClass() {
        this.showDivPokemon = !this.showDivPokemon
      },

      toggleClassSinglePokemon() {
        this.showDivSinglePokemon = !this.showDivSinglePokemon
      },

    
      
      countPokemonsNames() {
        console.log("countPokemonsNames", this.infoPokemons )
          let totalPokemonsNames = 0;
          if (this.infoPokemons == undefined) {
            return totalPokemonsNames;
          }
            totalPokemonsNames = this.infoPokemons.length
            console.log("THIS IS THE TOTAL:", totalPokemonsNames)
          return totalPokemonsNames;
      },

        listPokemonsImages() {
        let totalPokemonsNames = this.countPokemonsNames();
        let apiLink = "https://pokeapi.co/api/v2/pokemon-form/";
        console.log("THIS IS THE LENGHTTTTTT", totalPokemonsNames);
          let arrayPokemons = [];
          var pokemons = 0;
          for (var i = 1; i < totalPokemonsNames; i++) {
            var pokemons = apiLink  + i + "/";
            console.log("THIS IS MY STRING", pokemons);
            arrayPokemons.push(pokemons);
          }
            console.log("THIS IS THE ARRAY WITH POKEMONS:", arrayPokemons)
             return arrayPokemons;
      },
    },
    
      created() {
        let infoPokemons = this.getPokemons();
        console.log("THESE ARE MY POKEMONS: ", this.infoPokemons)
        let imagesPokemons = this.getPokemonsImages();
        console.log("THESE ARE MY IMAGES: ", this.imagesPokemons)
      },
  }
</script>

<style>


  
</style>
