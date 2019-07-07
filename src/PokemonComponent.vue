<template>
    <div>
        <v-card class="ma-5" color="#26c6da" dark max-width="400" >
            <v-card-title>
            <v-icon left>create</v-icon>
            <span class="title font-weight-light">Name: </span><h2 class="ml-2">{{pokemonName}}</h2>
            </v-card-title>

            <v-card class="blue lighten-4"  width="350px">
                <v-layout width="300px" align-center justify-center><img :src="linksForImages" width="200px" height="200px" /></v-layout >
            </v-card>

            <v-card-actions>
            <v-list-tile class="grow">
                    <v-layout align-center justify-start>
                        <v-icon class="mr-1">star</v-icon>
                        <v-icon class="ml-2">thumb_up_alt</v-icon>
                    </v-layout>

                    <v-layout align-center justify-end>
                        <v-icon class="mr-1">favorite</v-icon>
                        <span class="subheading mr-2">256</span>
                        <v-icon class="mr-1">share</v-icon>
                        <span class="subheading">SHARE</span>
                    </v-layout>
            </v-list-tile>
            </v-card-actions>
        </v-card>    
    </div>
</template>

<script>
    export default {


        props: {
            pokemonName: String,
            pokemonUrl: String,
            indexProp: Object,
        },

        data() {
            return {
                linksForImages: "",
            }
        },

        created() {
        console.log('I am the INDEX', this.indexProp);
            let linkImages = this.getLinksForImages();
            console.log("THIS IS THE LINK FOR THE IMAGES IN CREATED", this.linkImages)
        },

        watch: {
            linksForImages() {
                console.log("I am changeddddd:",this.linksForImages);
                this.getImagesFromApi() 
            
            } 
        },

        methods: {
            getLinksForImages() {
                const axios = require('axios');
                console.log("THIS IS THE URLLLL", this.indexProp.url)
                axios.get(this.indexProp.url)
                .then(response => (this.linksForImages = response.data.forms[0].url));
            
            },
            
            getImagesFromApi() {
                const axios = require('axios');
                    console.log("THIS IS THE LINKKKKKKKK FOR IMAGES", this.linksForImages)
                    axios.get(this.linksForImages)
                    .then(response => (this.linksForImages = response.data.sprites.front_default))
                    .catch(function (error) {
                    console.log("THIS IS THE ERROR:",error);
                })
            }
        }     
    }
 
</script>

<style>
  #align-center {
      display: flex;
      align-items: center;
      justify-content: center; 
  }
</style>


