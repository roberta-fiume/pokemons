<template>
    <div>
     <div v-for="pokemon in infoPokemonsProp" :key="pokemon.name">
        <h2><a v-bind:href="pokemon.url">NAME: {{pokemon.name}}</a></h2> 
      </div>
      <div v-for="image in imagesArray" :key="image.front_default">
          <h2><a v-bind:href="image.url"> IMAGE: {{image.front_default}}</a></h2>
      </div>
    </div>
</template>

<script>



export default {
    props: ['infoPokemonsProp', 'imagesPokemonsProp'],



    data() {
        return {
            imagesArray: []
        }
    },

    watch: {
        imagesPokemonsProp() {
            this.imagesArray = this.imagesPokemonsProp
            console.log("I am changeddddd:",this.imagesArray)
        }
    },

    created() {
       this.imagesArray = this.imagesPokemonsProp
        console.log("THIS IS MY IMAGE PROP:", this.imagesArray)
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