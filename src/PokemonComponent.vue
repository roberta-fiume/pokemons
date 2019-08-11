<template>
    <div> 
        <v-card class="ma-5 card" color="grey darken-3" dark max-width="400px" max-height="500px" >
          
            <v-card width="380px">
                <v-layout class="300px" align-center justify-center><img :src="linksForImages" width="200px" height="200px" :class="{scaleClass:scaleClass, notScaled:notScaled}"/></v-layout >
            </v-card>
             <v-card-title class="v-card_title">
                <v-icon left small>create</v-icon>
                <span class="title font-weight-light">Name: </span><h3 class="title ml-2">{{pokemonName}}</h3>
            </v-card-title>
             
            <v-card-actions class="v-card_actions">
                <v-list-tile class="grow">
                        <v-layout align-center justify-start class="v-list_title">
                            <v-btn icon>
                                <v-icon class="pa-0" small>star</v-icon>
                            </v-btn>
                            
                            <v-btn icon>
                                <v-icon small>thumb_up_alt</v-icon>
                            </v-btn>
                        
                        </v-layout>

                        <v-layout align-center justify-end>
                            <v-btn icon>
                                <v-icon small>favorite</v-icon>
                            </v-btn>
                        
                        <v-btn icon >
                            <v-icon small>share</v-icon>
                            </v-btn>
                            <span class="body-1 ml-1">SHARE</span>
                        </v-layout>
                </v-list-tile>
            </v-card-actions>

         
        </v-card>  

    </div>
</template>

<script>
import model from './model.js'
import { EventBus } from '@/eventBus.js';


    export default {

        props: {
            pokemonName: String,
            pokemonUrl: String,
            indexProp: Object,
            index: Number,
            realIndexProp: Number
        },

        data() {
            return {
                linksForImages: "",
                scaleClass: false,
                notScaled: false,
                currentIndex: null
            }
        },

        created() {
        console.log('I am the OBJECTTTTT', this.indexProp);
        console.log('I am the realIndexProp', this.realIndexProp);
            let linkImages = this.getLinksForImages();
            // console.log("THIS IS THE LINK FOR THE IMAGES IN CREATED", this.linkImages)
        },

        mounted() {
            for (var i = 0; i < this.$refs.pokemonComponent.length; i++) {
                console.log("I AM THE INDEXXXX MALDITO IN MOUNTED:", this.$refs.pokemonComponent);
            }
            

        },


          updated(){
             console.log("I AM THE INDEXXXX MALDITO IN UPDATED:",this.$refs.pokemonComponent);
              EventBus.$on('i-got-clicked', scale => {
                  function scaleImg(index) {
                        if (index)  {
                            this.scaleClass = true;
                        } else {
                        this.scaleClass = false; 
                        }
                        console.log("I AM THE INDEX",this.currentIndex)
                        console.log("I AM FINALLY CHANGEEED",this.scaleClass)
                    }
                     const scaleImgFunc = scaleImg.bind(this);
                    scaleImgFunc(scale);
                });
           
            },
        
        
        watch: {
            linksForImages() {
                // console.log("I am changeddddd:",this.linksForImages);
                this.getImagesFromApi()
            },
            transform() {
                  console.log("I AM WATCHED AND TRANSFORMED", this.transform)
            }
        },

        methods: {
            getLinksForImages() {
                const axios = require('axios');
                // console.log("THIS IS THE URLLLL", this.indexProp.url)
                axios.get(this.indexProp.url)
                .then(response => (this.linksForImages = response.data.forms[0].url));
            
            },
            
            getImagesFromApi() {
                const axios = require('axios');
                    // console.log("THIS IS THE LINKKKKKKKK FOR IMAGES", this.linksForImages)
                    axios.get(this.linksForImages)
                    .then(response => (this.linksForImages = response.data.sprites.front_default))
                    .catch(function (error) {
                    console.log("THIS IS THE ERROR:",error);
                })
            },   
        }     
    }
 
</script>

<style lang="scss">

    #align-center {
      display: flex;
      align-items: center;
      justify-content: center; 
    }

    .v-list__tile {
        padding: 0px;
    }

    .v-card_title {
        margin-top: 10px;
        height: 45px;
    }

    .v-card_actions {
        height: 45px;
    }

   .layout {
    height: 300px;
   }

    .notScaled {
         width: 200px;
         height: 300px;
   }

   .scaleClass {
        transform: scale(1.3); 
   }

    .example {
        width: 300px;
        height: 300px;
    }

   
    //     #app{
    //         font-family: 'Avenir', Helvetica, Arial, sans-serif;
    //         -webkit-font-smoothing: antialiased;
    //         -moz-osx-font-smoothing: grayscale;
    //         text-align: center;
    //         color: #2c3e50;
    //         margin-top: 60px;

    // .demo {
    //     .glide {
    //       &__slide {
    //         display: flex;
    //         border: 2px solid #ccc;
    //         width: 450px;
    //         height: 450px;
    //         align-items: center;
    //         justify-content: center;
    //         color: #aaa;
    //         font-size: 36px;
    //         font-weight: 600;
    //         border-radius: 5px;
    //         transition: all .3s;
    //         opacity: .3;
    //         &--active {
    //           border: none;
    //           color: #fff;
    //            opacity: 1;
    //           background: linear-gradient(-45deg,#ed145b,#7b31f4);
    //           background-color: limegreen;
    //         }
    //       }
    //     }
    // }
    //}



</style>


