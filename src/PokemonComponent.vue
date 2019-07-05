<template>
    <div>
        <h2>{{pokemonName}}</h2>
          <v-img :src="linksForImages" width="200px" height="150px"></v-img>
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

