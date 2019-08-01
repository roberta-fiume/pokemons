<template>
    <div> 
        <v-card class="ma-5 card" color="grey darken-3" dark max-width="400" >
            <v-card-title>
                <v-icon left>create</v-icon>
                <span class="headline font-weight-light">Name: </span><h3 class="display-1 ml-2">{{pokemonName}}</h3>
            </v-card-title>

            <v-card class="purple lighten-5"  width="350px">
                <v-layout width="300px" align-center justify-center><img :src="linksForImages" width="200px" height="200px" /></v-layout >
            </v-card>

            <v-card-actions>
                <v-list-tile class="grow">
                        <v-layout align-center justify-start>
                            <v-btn icon>
                                <v-icon>star</v-icon>
                            </v-btn>
                            
                            <v-btn icon>
                                <v-icon>thumb_up_alt</v-icon>
                            </v-btn>
                        
                        </v-layout>

                        <v-layout align-center justify-end>
                            <v-btn icon>
                                <v-icon>favorite</v-icon>
                            </v-btn>
                        
                        <v-btn icon >
                            <v-icon>share</v-icon>
                            </v-btn>
                            <span class="body-1 ml-1">SHARE</span>
                
                        
                        </v-layout>
                </v-list-tile>
            </v-card-actions>
        </v-card>   



        <!-- <div class="container">
        <div class="owl-carousel">
            <div><img src="//placehold.it/400x300/936/fff/?text=1" alt=""></div>
            <div><img src="//placehold.it/400x300/693/fff/?text=2" alt=""></div>
            <div><img src="//placehold.it/400x300/369/fff/?text=3" alt=""></div>
            <div><img src="//placehold.it/400x300/f63/fff/?text=4" alt=""></div>
        </div>
        </div> -->

    </div>
</template>

<script>

    import carousel from '@/carousel.js'
    export default {


        props: {
            pokemonName: String,
            pokemonUrl: String,
            indexProp: Object,
        },

        data() {
            return {
                linksForImages: "",
                owlCarousel: ""
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

            // handleScroll(event) {
            //     this.hello();
            // },

        //  hello()  {
        //     document.getElementsByClassName('.owl-carousel').owlCarousel({
        //     autoplay: true,
        //     center: true,
        //     loop: true,
        //     nav: true,
        //     navText: ["<span class='icon icon-arrow-left7'></span>","<span class='icon icon-arrow-right7'></span>"],
        //     items: 1,
        //     responsive : {
        //     768 : {
        //         items : 3,
        //     }
        //     }
        //     })
        //  }
            
        }     
    }
 
</script>

<style>
    #align-center {
      display: flex;
      align-items: center;
      justify-content: center; 
    }

    /* .icon {
        background: rgba(255, 255, 255, .6);
        color: rgba(0, 0, 0, .3);
        font-family: 'FontAwesome';
        font-size: 40px;
        line-height: 60px;
        margin-top: -30px;
        position: absolute; top: 50%;
        text-align: center;
        width: 60px; height: 60px;
    }
    .owl-next, 
    .owl-prev {
        height: 100%;
        position: absolute;
        top: 0;
        width: 33.33333333%;
    }
    .owl-next {
        right: 0;
    }
    .owl-prev {
        left: 0;
    }
    .owl-next:hover .icon, 
    .owl-prev:hover .icon {
        background: rgba(48, 117, 70, .8);
        color: rgba(255, 255, 255, .9);
    }
    .icon-arrow-left7 { left: 0; }
    .icon-arrow-left7:before { content: "\f053"; }
    .icon-arrow-right7 { right: 0; }
    .icon-arrow-right7:before { content: "\f054"; }

@media (min-width: 768px) {
  .container { 
  
     margin: 0 auto;
    overflow: hidden;
    width: 700px;
  }
  .owl-carousel {
    margin: 0 -60px;
    position: relative;
    width: 820px;
  }
  .owl-item > div {
    margin: 45px 60px;
    transition: margin 400ms ease-out;
  }
  .owl-item.center > div {
    margin: 0;
  }
  .owl-next {
    right: 60px;
  }
  .owl-prev {
    left: 60px;
  }
  .icon-arrow-left7 { left: auto; right: 0; }
  .icon-arrow-right7{ left: 0; right: autp; }
}  */

 

</style>


