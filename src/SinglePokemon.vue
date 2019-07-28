<template>
    <div>
        <v-flex xs12>
            <v-card color="purple lighten-2" class="white--text">
              <v-card-title primary-title>
                <div>
                  <div class="body-2 mb-3" id="pokemonTitle">
                      <span class="title font-weight-light white--text text--lighten-2"> Name:</span>
                   <span class="title font-weight-bold white--text text--lighten-2 ml-1">{{pokemonName}}</span>
                  </div>
                  <div>
                       <video width="350" controls :src="singleVideo"></video>
                  </div>
                </div>
              </v-card-title>
              <v-card-actions>
                <v-btn flat dark  @click="goToPreviousPokemon" v-if="previousButton" class="white--text text--lighten-2">PREVIOUS</v-btn>
                <v-btn flat dark  @click="goToNextPokemon" v-if="nextButton"  class="white--text text--lighten-2">NEXT</v-btn>
              </v-card-actions>
            </v-card>
        </v-flex>
    </div>

 
 
</template>

<script> 
import firebase from 'firebase/app'
import db from '@/fb'

    export default {

        watch: {
            infoSinglePokemonProp() {
                console.log("I am changed:", this.infoSinglePokemonProp)
            },

            urlsCollection() {
                  this.orderUrls(); 
                  
                console.log("VIDEO COLLECTION IN WATCH", this.urlsCollection);
                this.singleVideo = this.urlsCollection[this.currentVideoIndex];
                console.log("THIS IS THE SINGLE VIDEO", this.singleVideo)
            }
          
          
        },
        
     
        mounted() {
            console.log("this is singleVideo in MOUNTED", this.singleVideo)
            this.currentPokemonIndex = 0;
            this.pokemonName = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
            console.log("THIS IS THE INDEX IN MOUNTED:", this.currentPokemonIndex);
            console.log("THIS IS THE POKEMON NAME:", this.pokemonName);
            console.log("THIS IS THE POKEMON NAME INDEXXX:", this.pokemonName);
            this.infoSinglePokemonProp;

            this.currentVideoIndex = 0;
            this.urlsCollection = this.getVideoCollection();
            console.log("VIDEO COLLECTION", this.urlsCollection);
           
            // this.singleVideo = this.docsVideos[this.currentVideoIndex];
            //   console.log("THIS IS DOCS VIDEOS", this.docsVideos);
            // console.log("THIS IS THE CONTEXT", this);
            // console.log("THIS IS THE CURRENT VIDEO INDEX", this.currentVideoIndex);
            // console.log("THIS IS THE SINGLE VIDEO", this.docsVideos[0]);
            // console.log("THIS IS SINGLE GIF", this.singleVideo)
       
            // var storage = firebase.storage();
            // let storageRef = storage.ref();
            // let videoRef = storageRef.child('videos/bulbasaur.mp4');
            //    function getVideosFromStorage() {
            //          videoRef.getDownloadURL().then(videoUrl => {
            //             this.singleVideo = videoUrl;
            //             console.log("THIS IS THE URL", videoUrl)
            //          })
            //          .catch(err => console.error(err));
            //         console.log("THIS AFTER API CALL", this);
            //     };
            //     const getVideosFromStorageFunc = getVideosFromStorage.bind(this);
            //     getVideosFromStorageFunc();
            // this.replaceStringsInUrl();
        },
        
        computed: {
        
        },
    
       props: ['infoSinglePokemonProp'],

       
        data() {
            return {
                currentPokemonIndex: "",
                pokemonName: "",
                previousButton: false,
                nextButton: true,
                // gifsArray: [
                // 'https://media.giphy.com/media/I2nZMy0sI0ySA/giphy.gif', 
                // 'https://media.giphy.com/media/GA3BbCXTEm6hq/giphy.gif', 
                // 'https://media.giphy.com/media/905ATvUcKqN0I/giphy.gif',
                // 'https://media.giphy.com/media/yhfTY8JL1wIAE/giphy.gif',
                // 'https://pkmneclipse.net/images/letsgo/kanto-normal/Charmeleon.gif',
                // 'https://media.giphy.com/media/48cVVAf9vam9W/giphy.gif', 
                // 'https://media.giphy.com/media/fjgqYjVkzfQ9a/giphy.gif', 
                // 'https://media.giphy.com/media/jymDyv7MzGgzC/giphy.gif',
                // 'https://media.giphy.com/media/tDT5nL8EXbQhW/giphy.gif',
                // 'https://media.giphy.com/media/ZKaR6dsqUELIs/giphy.gif',
                // 'https://pkmneclipse.net/images/letsgo/kanto-normal/Metapod.gif',
                // 'https://media.giphy.com/media/Ktr7TBN3hV39u/giphy.gif',
                // 'https://media.giphy.com/media/anLxZPExDZZ4I/giphy.gif',
                // 'https://pkmneclipse.net/images/letsgo/kanto-normal/Kakuna.gif', 
                // 'https://pkmneclipse.net/images/letsgo/kanto-normal/Beedrill.gif', 
                // 'https://pkmneclipse.net/images/letsgo/kanto-normal/Pidgey.gif', 
                // 'https://media.giphy.com/media/hJugcAt6VIzMA/giphy.gif', 
                // 'https://pkmneclipse.net/images/letsgo/kanto-normal/Pidgeot.gif', 
                // 'https://pkmneclipse.net/images/letsgo/kanto-normal/Rattata.gif', 
                // 'https://pkmneclipse.net/images/letsgo/kanto-normal/Raticate.gif'
                // ],
                singleVideo: "hello",
                currentVideoIndex: "",
                ideosUrls: [],
                docsVideos: [],
                urlsCollection: [],
                pokemons: ["bulbasaur", "ivysaur", "venusaur", "charmander", "charmeleon", "charizard", "squirtle", "wartortle", "blastoise",
                "caterpie", "metapod", "butterfree", "weedle", "kakuna", "beedrill", "pidgey", "pidgeotto", "rattata", "raticate" ] 
             
            }
        },

        methods: {

            //    countPokemonsNames() {
            //         console.log("countPokemonsNames", this.infoSinglePokemonProp)
            //         let totalPokemonsNames = 0;
            //             if (this.infoSinglePokemonProp == undefined) {
            //                 return totalPokemonsNames;
            //             }
            //             totalPokemonsNames = this.infoSinglePokemonProp.length
            //             console.log("THIS IS THE TOTAL:", totalPokemonsNames)
            //             return totalPokemonsNames;
            //     },
         
            goToNextPokemon() {
                this.currentPokemonIndex++;
                this.previousButton = true;
                // let totalPokemonsNames =  this.countPokemonsNames();
                console.log("THIS IS THE POKEMON NAMEEEEEE BEFORE", this.infoSinglePokemonProp[this.currentPokemonIndex].name)
                let pokemonName  = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
                console.log("THIS IS THE CURRENT POKEMON INDEX IN NEXT:", this.currentPokemonIndex)
                console.log("THIS IS THE CURRENT POKEMON NAME IN NEXT:", pokemonName )
                this.pokemonName = pokemonName;
                this.goToNextVideo();

                if (this.pokemonName === "raticate") {
                    this.nextButton = false;
                }
                return this.pokemonName
            },

               goToPreviousPokemon(){
                    this.currentPokemonIndex--; 
                    let pokemonName = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
                    this.pokemonName = pokemonName;
                    console.log("THIS IS THE CURRENT POKEMON INDEX IN  PREVIOUS:", this.currentPokemonIndex)
                    console.log("THIS IS THE CURRENT POKEMON NAME IN  PREVIOUS:", this.pokemonName);

                    this.goToPreviousVideo();

                        if (this.pokemonName === "bulbasaur") {
                            this.previousButton = false;
                        }
                    this.nextButton = true;
                },

                goToNextVideo() {
                    this.currentVideoIndex++;
                    let singleVideo  = this.gifsArray[this.currentVideoIndex];
                    console.log("THIS IS THE CURRENT GIF INDEX IN NEXT:", this.currentVideoIndex)
                    console.log("THIS IS THE CURRENT POKEMON GIF IN NEXT:", singleVideo )
                    this.singleVideo = singleVideo;   
                },

                goToPreviousVideo(){
                    this.currentVideoIndex--; 
                    let singleVideo = this.gifsArray[this.currentVideoIndex];
                    this.singleVideo = singleVideo; 
                    console.log("THIS IS THE CURRENT GIF INDEX IN  PREVIOUS:", this.currentVideoIndex)
                    console.log("THIS IS THE CURRENT GIF IN  PREVIOUS:", this.singleVideo);
                  
                },

                getVideoCollection() {
                    db.collection('pokemons').get().then((response) => {
                    // console.log("THIS IS THE response", response);
                    // console.log("THIS IS THE DOC", response.docs);
                    
                    // console.log("THIS IS THE URL",response.docs[0]._document.data.internalValue.root.value.internalValue);
                    for (var i=0; i < response.docs.length; i++) {
                        let urls = response.docs[i]._document.data.internalValue.root.value.internalValue;
                        console.log("URL IN LOOP",urls);
                           this.docsVideos.push(urls);
                    }
                     this.urlsCollection = this.docsVideos
                     console.log("URL COLLECTION IN FUNCTION", this.urlsCollection)
                    });

                    return this.urlsCollection
                },

                orderUrls() {
                    let bulbasaur = this.urlsCollection[0].replace("charmander", "bulbasaur");
                    console.log("BULBASAUR", bulbasaur);
                    let ivysaur = this.urlsCollection[1].replace("beedrill", "ivysaur");
                    console.log("IVYSAUR", ivysaur);
                    let venusaur = this.urlsCollection[2].replace("blastoise", "venusaur");
                    console.log("VENUSAUR", venusaur);
                    let charmander = this.urlsCollection[3].replace("bulbasaur", "charmander");
                    console.log("CHARMANDER", charmander);
                    let charmeleon = this.urlsCollection[4].replace("butterfree", "charmeleon");
                    console.log("CHARMELEON", charmeleon);
                    let charizard = this.urlsCollection[5].replace("caterpie", "charizard");
                    console.log("CHARIZARD", charizard);
        
                }

               

                
           

     
        }
  
    }
</script>

<style>

#div-pokemons {
    display: none;
};

#pokemonTitle {
    display: flex !important;
    flex-direction: row !important;
    align-items: center;
}


 

</style>
