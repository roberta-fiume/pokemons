<template>
    <div>
        <h2>{{pokemonName}}</h2>
        <!-- <v-img :src="image"  width="200px" height="150px"></v-img> -->
    </div>
</template>

<script>
export default {
    props: ['pokemonName','pokemonIndex'],
    data() {
        return {
            path: "https://raw.githubusercontent.com",
            imagesPokemons: "images",
            infoPokemons: "pokemons",

        }
    },

    created() {
       let pokemons = this.getPokemonsImages();
       console.log("Pokemonssssssssssss:", pokemons)
    },

    methods: {

    //     countPokemonsNames() {
    //     console.log("countPokemonsNames", this.infoPokemons )
    //       let totalPokemonsNames = 0;
    //       if (this.infoPokemons == undefined) {
    //         return totalPokemonsNames;
    //       }
    //         totalPokemonsNames = this.infoPokemons.length
    //         console.log("THIS IS THE TOTAL:", totalPokemonsNames)
    //       return totalPokemonsNames;
    //   },

    //     listPokemonsImages() {
    //       let totalPokemonsNames = this.countPokemonsNames();
    //       console.log("THIS IS THE LENGHTTTTTT", totalPokemonsNames);
    //       let arrayPokemons = [];
    //       var pokemons = 0;
    //       for (var i = 1; i < totalPokemonsNames; i++) {
    //         var pokemons = this.path + "/PokeAPI/sprites/master/sprites/pokemon/"+ i + ".png";
    //         // console.log("THIS IS MY STRING", pokemons);
    //         arrayPokemons.push(pokemons);
    //       }
    //       console.log("THIS IS THE ARRAY WITH POKEMONS:", arrayPokemons)
    //       return arrayPokemons;
    //   },

        getPokemonsImages() {
        console.log("I AM GET IN POKEMON COMPONENT");
        const axios = require('axios');
        axios.get('https://pokeapi.co/api/v2/pokemon-form/'+ pokemonIndex)
        .then(response => (this.imagesPokemons = response.data.result.url))
        .catch(function (error) {
        console.log("THIS IS THE ERROR:",error);
        })
        return this.imagesPokemons
      },
    }
    

       
}
 
</script>

