<template>
    <div>
        <v-container color="pink" row>
            <!-- <div id="pokemons-list">
                <div v-for="pokemon in infoPokemonsProp" :key="pokemon.name"  id="pokemons-names">
                    <h2><a v-bind:href="pokemon.url">NAME: {{pokemon.name}}</a></h2>  
                </div>
            </div> -->
         
                <v-flex xs12 sm6>
                    <v-card>
                        <v-container fluid grid-list-md>
                            <v-layout  width="200px" column wrap>
                                <v-flex v-for="pokemon in infoPokemonsProp" :key="pokemon" v-bind="{ [`xs${pokemon.flex}`]: true }">
                                    <v-card width="200px" height="200px"> 
                                    <span class="headline black--text" v-text="pokemon.name"></span>
                                    </v-card>
                                </v-flex>
                            </v-layout>
                        </v-container>
                    </v-card>
                </v-flex>
          
           
                <v-flex xs12 sm6>
                    <v-card width="250px">
                        <v-container fluid grid-list-md>
                            <v-layout column wrap>
                                <v-flex  v-for="image in imagesPokemonsProp" :key="image" v-bind="{ [`xs${image.flex}`]: true }">
                                    <v-card width="200px"> 
                                        <v-img :src="image"  width="200px" height="200px">
                                        </v-img>
                                        <v-card-actions>
                                            <v-spacer></v-spacer>
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
                                    </v-card>
                                </v-flex>
                            </v-layout>
                        </v-container>
                    </v-card>
                </v-flex>
           
        </v-container>
       

   


        


        
        <v-layout justify-center>
            <v-flex xs12 sm6>
                <v-card>
                    <v-container fluid grid-list-md>
                        <v-layout column wrap>
                            <v-flex v-for="card in cards" :key="card.title" v-bind="{ [`xs${card.flex}`]: true }">
                                <v-card> 
                                    <v-flex xs12 align-end flexbox>
                                        <span class="headline black--text" v-text="card.title"></span>
                                    </v-flex>
                                    <v-img :src="card.src" height="200px">
                                    </v-img>
                                    <v-card-actions>
                                        <v-spacer></v-spacer>
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
                                </v-card>
                            </v-flex>
                        </v-layout>
                    </v-container>
                </v-card>
            </v-flex>
        </v-layout>
    </div>
</template>

<script>



export default {
    props: ['infoPokemonsProp', 'imagesPokemonsProp'],
   



    data() {
        return {
            images: [],
            cards: [
        { title: 'Pre-fab homes', src: 'https://cdn.vuetifyjs.com/images/cards/house.jpg', flex: 6 },
        { title: 'Favorite road trips', src: 'https://cdn.vuetifyjs.com/images/cards/road.jpg', flex: 6 },
        { title: 'Best airlines', src: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg', flex: 6 }
      ]
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
    #pokemons-box {
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
  }

</style>