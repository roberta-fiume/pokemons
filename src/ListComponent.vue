<template>
    <div>
        <pokemon-component v-for="pokemon in infoPokemonsProp" :key="pokemon.name" :pokemonName="pokemon.name" :indexProp="pokemon"> </pokemon-component>
    </div>
</template> 

<script> 
import PokemonComponent from "./PokemonComponent.vue"


export default {
    props: ['infoPokemonsProp'],  
    components: {
       PokemonComponent 
    },

    data() {
        return {

        }
    },
}
</script>

