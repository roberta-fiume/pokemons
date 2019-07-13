<template>
    <div>
        <v-flex xs12>
            <v-card color="purple lighten-2" class="white--text">
              <v-card-title primary-title>
                <div>
                  <div class="body-1"><h2><a class="white--text"> Name: {{pokemonName}}</a></h2> </div>
                  <div class="gif-container">
                    <img :src="singleGif" />
                  </div>
                </div>
              </v-card-title>
              <v-card-actions>
                <v-btn flat dark   @click="goToPreviousPokemon" v-if="previousButton">PREVIOUS</v-btn>
                <v-btn flat dark  @click="goToNextPokemon" v-if="nextButton">NEXT</v-btn>
           
              </v-card-actions>
            </v-card>
        </v-flex>
    </div>

 
 
</template>

<script>

    export default {

        watch: {
            infoSinglePokemonProp() {
                console.log("I am changed:", this.infoSinglePokemonProp)
            }
        },
        
     
        mounted() {
            this.currentPokemonIndex = 0;
            this.pokemonName = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
            console.log("THIS IS THE INDEX IN MOUNTED:", this.currentPokemonIndex);
            console.log("THIS IS THE POKEMON NAME:", this.pokemonName);
            console.log("THIS IS THE POKEMON NAME INDEXXX:", this.pokemonName);

            this.infoSinglePokemonProp;

            this.currentGifIndex = 0;
            this.singleGif = this.gifsArray[this.currentGifIndex];
            console.log("THIS IS SINGLE GIF", this.singleGif)

        },
        
        computed: {
        
        },
    
       props: ['infoSinglePokemonProp'],

       
        data() {
            return {
                currentPokemonIndex: "",
                pokemonName: "",
                previousButton: false,
                nextButton: true,
                gifsArray: ['https://media.giphy.com/media/SfjCRiDNA951m/giphy.gif', 'https://media.giphy.com/media/GA3BbCXTEm6hq/giphy.gif', 'https://media.giphy.com/media/905ATvUcKqN0I/giphy.gif','https://media.giphy.com/media/yhfTY8JL1wIAE/giphy.gif', 'https://media.giphy.com/media/u1k1kpDZSw5sA/giphy.gif', 'https://media.giphy.com/media/48cVVAf9vam9W/giphy.gif', 'https://media.giphy.com/media/fjgqYjVkzfQ9a/giphy.gif', 'https://media.giphy.com/media/jymDyv7MzGgzC/giphy.gif', 'https://media.giphy.com/media/tDT5nL8EXbQhW/giphy.gif', 'https://media.giphy.com/media/ZKaR6dsqUELIs/giphy.gif', 'https://media.giphy.com/media/LG6QazCB6tOCI/giphy.gif'],
                singleGif: "",
                currentGifIndex: ""
              
            }
        },

        methods: {

            //    countPokemonsNames() {
            //         console.log("countPokemonsNames", this.infoSinglePokemonProp)
            //         let totalPokemonsNames = 0;
            //             if (this.infoSinglePokemonProp == undefined) {
            //                 return totalPokemonsNames;
            //             }
            //             totalPokemonsNames = this.infoSinglePokemonProp.length
            //             console.log("THIS IS THE TOTAL:", totalPokemonsNames)
            //             return totalPokemonsNames;
            //     },
         
            goToNextPokemon() {
                this.currentPokemonIndex++;
                this.previousButton = true;
                // let totalPokemonsNames =  this.countPokemonsNames();
                console.log("THIS IS THE POKEMON NAMEEEEEE BEFORE", this.infoSinglePokemonProp[this.currentPokemonIndex].name)
                let pokemonName  = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
                console.log("THIS IS THE CURRENT POKEMON INDEX IN NEXT:", this.currentPokemonIndex)
                console.log("THIS IS THE CURRENT POKEMON NAME IN NEXT:", pokemonName )
                this.pokemonName = pokemonName;
                this.goToNextGifPokemon();

                if (this.pokemonName === "raticate") {
                    this.nextButton = false;
                }
                return this.pokemonName
            },

               goToPreviousPokemon(){
                    this.currentPokemonIndex--; 
                    let pokemonName = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
                    this.pokemonName = pokemonName;
                    console.log("THIS IS THE CURRENT POKEMON INDEX IN  PREVIOUS:", this.currentPokemonIndex)
                    console.log("THIS IS THE CURRENT POKEMON NAME IN  PREVIOUS:", this.pokemonName);
                        if (this.pokemonName === "bulbasaur") {
                            this.previousButton = false;
                        }
                    this.nextButton = true;
                },

                goToNextGifPokemon() {
                    this.currentGifIndex++;
                    let singleGif  = this.gifsArray[this.currentGifIndex];
                    console.log("THIS IS THE CURRENT GIF INDEX IN NEXT:", this.currentGifIndex)
                    console.log("THIS IS THE CURRENT POKEMON GIF IN NEXT:", singleGif )
                    this.singleGif = singleGif;   
                }
        }
  
    }
</script>

<style>

#div-pokemons {
    display: none;
}
 

</style>
