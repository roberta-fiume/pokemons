<template>
    <div>
        <div v-for="pokemon in  infoSinglePokemonProp" id="div-pokemons">
         <br/>
        </div>

        <div>
             <h2><a>NAME: {{pokemonName}}</a></h2> 
       
                 <!-- <h2><a  v-bind:href="pokemon.url">NAME: {{infoSinglePokemonProp[0].name}}</a></h2>  -->
        </div>

     <div>
         <button @click="goToNextPokemon()">NEXT</button>
     </div>
    </div>
 
</template>

<script>

    export default {

        watch: {
            infoSinglePokemonProp() {
                console.log("I am changed:", this.infoSinglePokemonProp)
            }
        },
        
        created() {
       
           console.log("I AM CREATED AND MY VALUE IS: ",this.infoSinglePokemonProp);     
        },

        beforeUpdate() {
              console.log("AM I UPDATED?",this.infoSinglePokemonProp)
        },

        updated() {
            this.infoSinglePokemonProp;
            console.log(" I AM UPDATED",this.infoSinglePokemonProp)
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
                
                console.log("THIS IS MY PROP", pokemonName);
                this.pokemonName = pokemonName;
            }
        }
  
    }
</script>

<style>

#div-pokemons {
    display: none;
}
 
   .divSinglePokemon {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 300px;
    height: 100%;
    border: 2px solid rgb(52, 153, 216);
  }
</style>
