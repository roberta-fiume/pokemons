<template>
    <div>
        <v-container align-top justify-center row wrap width="750px" class="white" id="cont">
            <div width="250px" class="white" >
                <v-container fluid grid-list-md>
                    <v-layout column wrap>
                        <v-flex v-for="pokemon in infoPokemonsProp" :key="pokemon.name " v-bind="{ [`xs${pokemon.flex}`]: true }">
                            <div  id="card1">
                                <span class="headline grey--text" v-text="pokemon.name"></span>
                            </div>
                        </v-flex>
                    </v-layout>
                </v-container>
            </div>
            <div width="350px" class="white">
                <div fluid grid-list-md>
                    <v-layout column wrap class="align-center">
                        <v-flex v-for="image in imagesPokemonsProp" :key="image" v-bind="{ [`xs${image.flex}`]: true }">
                            <div width="200px" justify-center id="div-img" >
                                <v-img :src="image"  width="200px" height="150px">
                                </v-img>
                                <v-card-actions class="justify-center white" id="div-icons">
                                    <v-btn icon>
                                        <v-icon>favorite</v-icon>
                                    </v-btn>
                                    <v-btn icon>
                                        <v-icon>bookmark</v-icon>
                                    </v-btn>
                                    <v-btn icon>
                                        <v-icon>share</v-icon>
                                    </v-btn>
                                </v-card-actions>
                            </div>
                        </v-flex>
                    </v-layout>
                </div>
            </div>
        </v-container>

    </div>
</template>

<script>



export default {
    props: ['infoPokemonsProp', 'imagesPokemonsProp'],
   
    data() {
        return {
            images: [],
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
                axios.get(this.imagesPokemonsProp[i])
                    .then(response =>(this.images.push(response.data.sprites)))
                    .catch(function (error) {
                    console.log("THIS IS THE ERROR:",error);
                })
            }
            return this.images;
        }
    },

    mounted() {
        console.log("THIS IS MY IMAGE PROP IN MOUNTED:", this.imagesPokemonsProp)
    },

}
</script>


<style>

#cont {
    display: flex;
    flex-direction: row;
}

#card1{
 
    width: 200px;
    height: 202px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
}

#div-img {
    /* border: 2px solid #E1BEE7;
   border: 2px solid #EA80FC; */

}

#div-icons {
    border: 2px solid #E1BEE7;
}
    /* #pokemons-box {
    display: flex;
    flex-direction: row;
    width: 600px;
    flex-wrap: wrap;
    height: 100%;
    align-items: center;
    border: 2px solid lightcoral;
  }

  #pokemons-list {
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  #pokemons-names{
    width: 200px;
    height: 200px;
    display: flex;
    flex-direction: column;
    border: 2px solid blue;
  }

    #img {
        width: 170px;
        height: 170px;
        border: 2px solid green;
    }
  #pokemons-div-img {
    display: flex;
    flex-direction: column;
    height: 100%; 
  }

  #pokemons-img {
    margin-top: 0px;
    width: 210px;
    height: 210px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 2px solid pink;
  } */

</style>
