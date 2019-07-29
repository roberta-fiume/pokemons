<template>
  <v-app class="purple lighten-5" >
      

       <div class="wrap-div ma-5">
          <div v-if="showDivSinglePokemon">
            <SinglePokemon :infoSinglePokemonProp="infoPokemons" />
          </div>

          <div class="purple lighten-2" id="scroll-box" v-if="showDivPokemon">
              <ListComponent :infoPokemonsProp="infoPokemons"/>
          </div>
       </div>

      <v-layout v-if="layout">
        <v-flex xs12 sm12 lg6 offset-sm3>
          <v-card>
            <v-img :src="images.mainImg" class="img"></v-img>

            <v-card-title   primary-title id="title">
              <div>
                <h3 class="headline mb-0">Welcome to Pokemons' App</h3>
              </div>
            </v-card-title>

            <v-card-actions id="wrap-button"> 
              <v-btn block flat class="purple accent-1" @click="showPokemons()" >Get Pokemons</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
  </v-app>
</template>

<script>

  import SinglePokemon from "./SinglePokemon.vue"
  import ListComponent from "./ListComponent.vue"

  export default {



    name: 'App',
     components: {
      ListComponent,
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
        layout: true    
      }
    },

    methods: {
      getPokemonsNames() {
        console.log("Hello, I work! I am GET POKEMONS");
        const axios = require('axios');
        axios.get('https://pokeapi.co/api/v2/pokemon/')
        .then(response => (this.infoPokemons = response.data.results))
        .catch(function (error) {
        console.log("THIS IS THE ERROR:",error);
        })
        return this.infoPokemons
      },

      // getPokemonsImages() {
      //   console.log("Hello, I workkkkkkk!");
      //   const axios = require('axios');
      //   let arrayPokemons =  this.listPokemonsImages();
      //   console.log('THESE IS THE ARRAY IMAGEEEEESSSSS', this.imagesPokemons)
      //   axios.get('https://pokeapi.co/api/v2/pokemon-form/1/')
      //   .then(response => (this.imagesPokemons = arrayPokemons))
      //   .catch(function (error) {
      //   console.log("THIS IS THE ERROR:",error);
      //   })
      //   return this.imagesPokemons
      // },

      showPokemons() {
        this.layout = !this.layout
        this.toggleClass();
        this.toggleClassSinglePokemon()
      },

      toggleClass() {
        this.showDivPokemon = !this.showDivPokemon
      },

      toggleClassSinglePokemon() {
        this.showDivSinglePokemon = !this.showDivSinglePokemon
      },

      // countPokemonsNames() {
      //   console.log("countPokemonsNames", this.infoPokemons )
      //     let totalPokemonsNames = 0;
      //     if (this.infoPokemons == undefined) {
      //       return totalPokemonsNames;
      //     }
      //       totalPokemonsNames = this.infoPokemons.length
      //       console.log("THIS IS THE TOTAL:", totalPokemonsNames)
      //     return totalPokemonsNames;
      // },

    },
    
      created() {
        let infoPokemons = this.getPokemonsNames();
        console.log("THESE ARE MY POKEMONS: ", this.infoPokemons)
      },
  }
</script>

<style>

.wrap-div {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

#title {
  display: flex;
  justify-content: column;
  align-items: center;
  justify-content: center;
}

#wrap-button {
  display: flex;
  justify-content: column;
  align-items: center;
  justify-content: center;
}

#scroll-box {
  height: 630px;
  overflow-y: scroll;
}
  
</style>
