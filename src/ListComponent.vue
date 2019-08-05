<template>
    <div id="app">
 
      <vue-glide class="demo" :bullet="true">
      <vue-glide-slide
        v-for="i in 10"
        :key="i">
        Slide {{ i }}
      </vue-glide-slide>
      <template slot="control">
        <button data-glide-dir="<" class="controls">prev</button>
        <button data-glide-dir=">" class="controls">next</button>
      </template> 

      <div data-glide-el="controls[nav]">
          <button data-glide-dir="=0" ></button>
          <button data-glide-dir="=1"></button>
          <button data-glide-dir="=2"></button>
          <button data-glide-dir="=3"></button>
          <button data-glide-dir="=4"></button>
          <button data-glide-dir="=5"></button>
          <button data-glide-dir="=6"></button>
          <button data-glide-dir="=7"></button>
          <button data-glide-dir="=8"></button>
          <button data-glide-dir="=9"></button>
          </div>
    </vue-glide>
        <!-- <pokemon-component v-for="pokemon in infoPokemonsProp" :key="pokemon.name" :pokemonName="pokemon.name" :indexProp="pokemon"> </pokemon-component> -->
    </div>
</template> 

<script> 
// var sass = require('node-sass');

// sass.render({
//   file: scss_filename,
 
// }, function(err, result) { /*...*/ });

import PokemonComponent from "./PokemonComponent.vue"
import VueGlide from './components/Glide'
import VueGlideSlide from './components/GlideSlide'



export default {
    props: ['infoPokemonsProp'],  
    components: {
       PokemonComponent,
    [VueGlide.name]: VueGlide,
    [VueGlideSlide.name]: VueGlideSlide
    },

    data() {
        return {

        }
    },
}
</script>
<style lang="scss">
    #scroll {
        display: flex;
        flex-direction: row;
        align-items: center;
        overflow-x: scroll;
    }
#app{
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

.demo {
    .glide {
      &__slide {
        display: flex;
        border: 2px solid #ccc;
        height: 200px;
        align-items: center;
        justify-content: center;
        color: #aaa;
        font-size: 36px;
        font-weight: 600;
        border-radius: 5px;
        transition: all .3s;
        opacity: .3;
        &--active {
          border: none;
          color: #fff;
           opacity: 1;
          background: linear-gradient(-45deg,#ed145b,#7b31f4);
          background-color: limegreen;
        }
      }
    }

   .controls {
    font-size: 18px;
    position: absolute;
    border: 0;
    outline: 0;
    padding: 10px;
    border-radius: 3px;
    background-color: blue;
    opacity: 0.5;
    color: white;
    cursor: pointer;
    width: 70px;
    height: 70px;
}

button[data-glide-dir="<"] {
    left: 5px;
}

button[data-glide-dir=">"] {
    right: 5px;
}

.glide__bullet {
        background-color: yellow;
    border-style: none;
    color: inherit;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    margin: 10px;
}


  }
}


</style>


