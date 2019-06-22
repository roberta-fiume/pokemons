<template>
    <div>
     <div v-for="pokemon in infoPokemonsProp" :key="pokemon.name">
        <h2><a v-bind:href="pokemon.url">NAME: {{pokemon.name}}</a></h2> 
      </div>
      <div v-for="image in imagesPokemonsProp" :key="image.front_default">
              <img :src="path + 'PokeAPI/sprites/master/sprites/pokemon/'+ image.front_default + '.png'"/>
      </div>
    </div>
</template>

<script>



export default {
    props: ['infoPokemonsProp', 'imagesPokemonsProp'],
   



    data() {
        return {
            path: "https://raw.githubusercontent.com/",
            images: []
        }
    },

    watch: {
        imagesPokemonsProp() {
            console.log("I am changeddddd:",this.imagesPokemonsProp);
      
        }
     
    },

    methods: {
        getImagesFromApi() {
            const axios = require('axios');
            for (var i = 0; i < this.imagesPokemonsProp.length; i ++) {
                console.log("THIS THE PROP ARRAY IN FOR LOOP", this.imagesPokemonsProp);
                console.log("THIS IS THE IIIIIII", i);
                 console.log("THIS IS THE lengthhhhh", this.imagesPokemonsProp.length);
                axios.get(this.imagesPokemonsProp[i])
                    .then(response =>(this.images.push(response.data.sprites.front_default)))
                    .catch(function (error) {
                    console.log("THIS IS THE ERROR:",error);
                })
            }
            return this.images;
        }
    },

    created() {
        console.log("THIS IS MY IMAGE PROP IN CREATED:", this.imagesPokemonsProp)
    },


    updated() {
        let images = this.getImagesFromApi();
        console.log("THIS IS MY ARRAY OF IMAGESSSSSSSSSSSS", images)
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