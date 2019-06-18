<template>
    <div>
     <div v-for="pokemon in infoPokemonsProp">
        <h2><a  v-bind:href="pokemon.url">NAME: {{pokemon.name}}</a></h2> 
         <!-- <p> URL: {{pokemon.url}}</p> -->
         <br/>
      </div>
    </div>
</template>

<script>



export default {
    props: ['infoPokemonsProp'],

    methods: {
   
    }
}
</script>


<style>
    .divSeePokemons {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 300px;
    height: 100%;
    border: 2px solid lightcoral;
  }

</style>