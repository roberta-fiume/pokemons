<template>
    <div> 
        <v-card class="ma-5 card" color="grey darken-3" dark max-width="400px" max-height="500px" >
          
            <v-card width="380px">
                <v-layout class="300px" align-center justify-center><img :src="linksForImages" width="200px" height="200px"/></v-layout >
            </v-card>
             <v-card-title class="v-card_title">
                <v-icon left small>create</v-icon>
                <span class="title font-weight-light">Name: </span><h3 class="title ml-2">{{pokemonName }}</h3>
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
        
<!-- 
                 <vue-glide class="demo" :bullet="true">
                <vue-glide-slide v-for="i in 10" :key="i">
                    Slide {{ i }}
                </vue-glide-slide>

                <template slot="control">
                    <button data-glide-dir="<" class="controls">prev</button>
                    <button data-glide-dir=">" class="controls">next</button>
                </template> 

                <div data-glide-el="controls[nav]">
                    <button data-glide-dir="=0" ></button>
                    <button data-glide-dir="=1"></button>
                    <button data-glide-dir="=2"></button>
                    <button data-glide-dir="=3"></button>
                    <button data-glide-dir="=4"></button>
                    <button data-glide-dir="=5"></button>
                    <button data-glide-dir="=6"></button>
                    <button data-glide-dir="=7"></button>
                    <button data-glide-dir="=8"></button>
                    <button data-glide-dir="=9"></button>
                    </div>
        </vue-glide> 
        
        -->

    </div>
</template>

<script>

    export default {

        components: {
           
        },

        props: {
            pokemonName: String,
            pokemonUrl: String,
            indexProp: Object,
        },

        data() {
            return {
                linksForImages: "",
                owlCarousel: "",
               
            }
        },

        created() {
        // console.log('I am the INDEX', this.indexProp);
            let linkImages = this.getLinksForImages();
            // console.log("THIS IS THE LINK FOR THE IMAGES IN CREATED", this.linkImages)

             window.addEventListener('scroll', this.handleScroll);
        },

        destroyed () {
            window.removeEventListener('scroll', this.handleScroll);
        },

        watch: {
            linksForImages() {
                // console.log("I am changeddddd:",this.linksForImages);
                this.getImagesFromApi() 
            
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


