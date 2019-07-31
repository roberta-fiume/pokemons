<template>
  <v-app class="black" id="background">
      <div id="wrapper-title" v-if="layout" >
        <svg viewBox="0 0 600 300">
         
          <symbol id="s-text">
            <text text-anchor="middle"
                  x="50%" y="50%" dy=".35em">
              Pokemon
            </text>

          
          </symbol>  
   
          <use xlink:href="#s-text" class="text"></use>
          <use xlink:href="#s-text" class="text"></use>
          <use xlink:href="#s-text" class="text"></use>
          <use xlink:href="#s-text" class="text"></use>
          <use xlink:href="#s-text" class="text"></use>
        </svg>


          <img :src="images.mainImg" id="image"/>
          <div id="flex-div">
            <h1 class="display-1 font-weight-medium white--text" id="h1"  @click="showPokemons" > get them all</h1>
            <img :src="images.pokemonBall" id="pokemon-ball" alt="">
          </div>
        </div>
   
      
    
       <div class="wrap-div ma-5">
          <div v-if="showDivSinglePokemon" id="singlePokemonBox">
            <SinglePokemon :infoSinglePokemonProp="infoPokemons" />
          </div>

          <div class="grey darken-1" id="scroll-box" v-if="showDivPokemon">
              <ListComponent :infoPokemonsProp="infoPokemons"/>
          </div>
       </div>


       <!-- <v-layout v-if="layout" >
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
      </v-layout>  -->

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
        mainImg: require('./assets/img/pokemons1.jpg'),
        pokemonBall: require('./assets/img/poke-ball.png'),
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

    },
    
      created() {
        let infoPokemons = this.getPokemonsNames();
        console.log("THESE ARE MY POKEMONS: ", this.infoPokemons)
      },
  }
</script>

<style>

@import url(http://fonts.googleapis.com/css?family=Open+Sans:800);

html {
  height: 100%;
}

body {
  height: 100%;
}

#image {
  opacity: 0.2;
  height: 100%;
}

#pokemon-ball {
  display: flex;
  position: absolute; 
  height: 40px;
  width: 40px;
  left: 58%;
  top: 72.3%;
}

#wrapper-title{
  display: flex;
  justify-content: center;
  position: relative;
  left: 50%;                     
  top: 50%;                        
  transform: translate(-50%, -50%);
}


 h1 {
  display: flex;
  position: absolute;  
  left: 50%;                       
  top: 75%;                      
  transform: translate(-50%, -50%);
  text-transform: uppercase;
}

#h1:hover {
  color: yellow !important;
}

#singlePokemonBox {
  margin-bottom: 50px;
}

  /* .wrap-div {
  display: none;
  flex-direction: column;
  justify-content: space-evenly; 
}   */

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
  

 .text {
  fill: none;
  stroke-width: 6;
  stroke-linejoin: round;
  stroke-dasharray: 70 330;
  stroke-dashoffset: 0;
  -webkit-animation: stroke 6s infinite linear;
  animation: stroke 6s infinite linear;
}

.text:nth-child(5n + 1) {
  stroke: #F2385A;
  -webkit-animation-delay: -1.2s;
  animation-delay: -1.2s;
}
.text:nth-child(5n + 2) {
  stroke: #F5A503;
  -webkit-animation-delay: -2.4s;
  animation-delay: -2.4s;
} 

.text:nth-child(5n + 3) {
  stroke: #E9F1DF;
  -webkit-animation-delay: -3.6s;
  animation-delay: -3.6s;
}

.text:nth-child(5n + 4) {
  stroke: #56D9CD;
  -webkit-animation-delay: -4.8s;
  animation-delay: -4.8s;
}

.text:nth-child(5n + 5) {
  stroke: #3AA1BF;
  -webkit-animation-delay: -6s;
  animation-delay: -6s;
} 

@-webkit-keyframes stroke {
  100% {
    stroke-dashoffset: -400;
  }
}

@keyframes stroke {
  100% {
    stroke-dashoffset: -400;
  }
}

html, body {
  height: 100%;
}

body {
 background: #111;
  background-size: .2em 100%;
  font: 7.5em/1 Open Sans, Impact;
  margin: 0;
} 

svg {
  position: absolute;
  width: 100%;
  height: 100%;
}     
</style>
