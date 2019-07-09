<template>
    <div>
        <v-flex xs12>
            <v-card color="purple lighten-2" class="white--text">
              <v-card-title primary-title>
                <div>
                  <div class="body-1"><h2><a class="white--text"> Name: {{pokemonName}}</a></h2> </div>
                  <span>Listen to your favorite artists and albums whenever and wherever, online and offline.</span>
                </div>
              </v-card-title>
              <v-card-actions>
                <v-btn flat dark   @click="goToPreviousPokemon">PREVIOUS</v-btn>
                <v-btn flat dark  @click="goToNextPokemon">NEXT</v-btn>
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
            this.currentPokemonIndex++;
            this.infoSinglePokemonProp;
            console.log(" I AM MOUNTED",this.infoSinglePokemonProp)
        },
        
        computed: {
        
        },
    
       props: ['infoSinglePokemonProp'],

       
        data() {
            return {
                currentPokemonIndex: "",
                pokemonName: ""
            
            }
        },

        methods: {
         
            goToNextPokemon() {
                let pokemonName = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
                this.currentPokemonIndex++;
                console.log("THIS IS THE CURRENT POKEMON INDEX IN NEXT:", this.currentPokemonIndex)

                console.log("THIS IS MY PROP", pokemonName);
                this.pokemonName = pokemonName;

                if (pokemonName === "raticate") {
                    this.currentPokemonIndex = 0;
                    this.currentPokemonIndex++;
                }
            },

               goToPreviousPokemon() {
                let pokemonName = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
                this.currentPokemonIndex--;

                console.log("THIS IS MY PROP in previous", pokemonName);

                console.log("THIS IS THE CURRENT POKEMON INDEX IN  PREVIOUS:", this.currentPokemonIndex)

                this.pokemonName = pokemonName;

                 if (pokemonName === "bulbasaur") {
                    this.currentPokemonIndex = 0;
                    this.currentPokemonIndex--;
                }
            },


        }
  
    }
</script>

<style>

#div-pokemons {
    display: none;
}
 

</style>
