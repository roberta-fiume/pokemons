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
                       <video width="350" controls :src="singleGif"></video>
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
import fb from '@/fb'

    export default {

        watch: {
            infoSinglePokemonProp() {
                console.log("I am changed:", this.infoSinglePokemonProp)
            },

            singleGif() {
                   let linksUrls = [];
                    let pokemons = ['ivysaur', 'venusaur', 'charmander'];
                    for (let i = 0; i < pokemons.length; i++) {
                       let newUrl = this.singleGif.replace("bulbasaur", pokemons[i]);
                        linksUrls.push(newUrl);
                    } 
                 console.log("I AM THE URLS ARRAY:", linksUrls) 
            }
          
          
        },
        
     
        mounted() {
            console.log("this is singleGif in MOUNTED", this.singleGif)
            this.currentPokemonIndex = 0;
            this.pokemonName = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
            console.log("THIS IS THE INDEX IN MOUNTED:", this.currentPokemonIndex);
            console.log("THIS IS THE POKEMON NAME:", this.pokemonName);
            console.log("THIS IS THE POKEMON NAME INDEXXX:", this.pokemonName);
            this.infoSinglePokemonProp;

            this.currentGifIndex = 0;
            // this.singleGif = this.gifsArray[this.currentGifIndex];
            // console.log("THIS IS SINGLE GIF", this.singleGif)
       
            var storage = firebase.storage();
            let storageRef = storage.ref();
            let videoRef = storageRef.child('videos/bulbasaur.mp4');
               function getVideosFromStorage() {
                     videoRef.getDownloadURL().then(videoUrl => {
                        this.singleGif = videoUrl;
                        console.log("THIS IS THE URL", videoUrl)
                     })
                     .catch(err => console.error(err));
                    console.log("THIS AFTER API CALL", this);
                };
                const getVideosFromStorageFunc = getVideosFromStorage.bind(this);
                getVideosFromStorageFunc();
            this.replaceStringsInUrl();
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
                singleGif: "hello",
                currentVideoIndex: "",
                pokemons: []
             
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
                this.goToNextGifPokemon();

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

                    this.goToPreviousGif();

                        if (this.pokemonName === "bulbasaur") {
                            this.previousButton = false;
                        }
                    this.nextButton = true;
                },

                goToNextGifPokemon() {
                    this. currentVideoIndex++;
                    let singleGif  = this.gifsArray[this.currentGifIndex];
                    console.log("THIS IS THE CURRENT GIF INDEX IN NEXT:", this.currentGifIndex)
                    console.log("THIS IS THE CURRENT POKEMON GIF IN NEXT:", singleGif )
                    this.singleGif = singleGif;   
                },

                goToPreviousGif(){
                    this.currentGifIndex--; 
                    let singleGif = this.gifsArray[this.currentGifIndex];
                    this.singleGif = singleGif; 
                    console.log("THIS IS THE CURRENT GIF INDEX IN  PREVIOUS:", this.currentGifIndex)
                    console.log("THIS IS THE CURRENT GIF IN  PREVIOUS:", this.singleGif);
                  
                },

                replaceStringsInUrl() {
          
                    console.log("THIS IS BULBASAUR", this.singleGif);
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
