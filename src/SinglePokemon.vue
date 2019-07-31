<template>
    <div>
        <v-flex xs12>
            <v-card color="purple lighten-2" class="white--text">
               
                    <v-card-title class="justify-center">
                        <div>
                            <h2 class="display-1 font-weight-medium white--text mt-4"><v-icon class="mr-2">remove_red_eye</v-icon>WATCH THEM ALL</h2>
                            <div class="body-2 ma-4" id="pokemonTitle">
                                <span class="title font-weight-light white--text text--lighten-2"> Name:</span>
                            <span class="title font-weight-bold white--text text--lighten-2 ml-1">{{pokemonName}}</span>
                            </div>
                            <v-flex>
                                <video flex width="700px" height="500px" controls :src="singleVideo"></video>
                            </v-flex>

                                     <v-card-actions>
                        <v-btn flat dark  @click="goToPreviousPokemon" v-if="previousButton" class="white--text text--lighten-2">PREVIOUS</v-btn>
                        <v-btn flat dark  @click="goToNextPokemon" v-if="nextButton"  class="white--text text--lighten-2">NEXT</v-btn>
                    </v-card-actions>
                        </div>

                   
                    </v-card-title>
                
                
             
            </v-card>
            
        </v-flex>
    </div>

 
 
</template>

<script> 
import firebase from 'firebase/app'
import db from '@/fb'

    export default {

        watch: {
         
            urlsCollection() {
                let pokemonsUrls = this.orderUrls();  
                this.singleVideo = pokemonsUrls[this.currentVideoIndex];
                console.log("THIS IS THE SINGLE VIDEO", this.singleVideo)  
            } 
        },
        
     
        mounted() {
            this.currentPokemonIndex = 0;
            this.pokemonName = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
            this.infoSinglePokemonProp;
            this.currentVideoIndex = 0;
            this.urlsCollection = this.getVideoCollection(); 
        },
        
       props: ['infoSinglePokemonProp'],

       
        data() {
            return {
                currentPokemonIndex: "",
                pokemonName: "",
                previousButton: false,
                nextButton: true,
                singleVideo: "",
                currentVideoIndex: "",
                docsVideos: [],
                urlsCollection: [],
                pokemons: ["bulbasaur", "ivysaur", "venusaur", "charmander", "charmeleon", "charizard", "squirtle", "wartortle", "blastoise",
                "caterpie", "metapod", "butterfree", "weedle", "kakuna", "beedrill", "pidgey", "pidgeotto", "rattata", "raticate" ] 
            }
        },

        methods: {
         
            goToNextPokemon() {
                this.currentPokemonIndex++;
                this.previousButton = true;
                let pokemonName  = this.infoSinglePokemonProp[this.currentPokemonIndex].name;
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
                    this.goToPreviousVideo();
                        if (this.pokemonName === "bulbasaur") {
                            this.previousButton = false;
                        }
                    this.nextButton = true;
                },

                getVideoCollection() {
                    db.collection('pokemons').get().then((response) => {
                    for (var i=0; i < response.docs.length; i++) {
                        let urls = response.docs[i]._document.data.internalValue.root.value.internalValue;
                        // console.log("URL IN LOOP",urls);
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
                    let squirtle = this.urlsCollection[6].replace("charizard", "squirtle");
                    console.log("SQUITLE", squirtle);
                    let wartortle = this.urlsCollection[7].replace("charmeleon", "wartortle");
                    console.log("WARTORTLE", wartortle);
                    let blastoise = this.urlsCollection[8].replace("ivysaur", "blastoise");
                    console.log("BLASTOISE", blastoise);
                    let caterpie = this.urlsCollection[9].replace("kakuna", "caterpie");
                    console.log("CATERPIE", caterpie);
                    let metapod = this.urlsCollection[10].replace("metapod", "metapod");
                    console.log("METAPOD", metapod );
                    let butterfree = this.urlsCollection[11].replace("pidgeot", "butterfree");
                    console.log("BUTTERFREE", butterfree);
                    let weedle = this.urlsCollection[12].replace("pidgeotto", "weedle");
                    console.log("WEEDLE",weedle);
                    let kakuna = this.urlsCollection[13].replace("pidgey", "kakuna");
                    console.log("KAKUNA", kakuna);
                    let beedrill = this.urlsCollection[14].replace("raticate", "beedrill");
                    console.log("BEEDRILL", beedrill);
                    let pidgey = this.urlsCollection[15].replace("rattata","pidgey");
                    console.log("PIDGEY", pidgey);
                    let pidgeotto = this.urlsCollection[16].replace("squirtle","pidgeotto");
                    console.log("PIDGEOTTO", pidgeotto);
                    let pidgeot = this.urlsCollection[17].replace("venusaur","pidgeot");
                    console.log("PIDGEOT", pidgeot);
                    let rattata = this.urlsCollection[18].replace("wartortle","rattata");
                    console.log("RATTATA", rattata);
                    let raticate = this.urlsCollection[19].replace("weedle","raticate");
                    console.log("RATICATE", raticate);

                    let pokemonsUrls = [];
                    pokemonsUrls.push(bulbasaur, ivysaur, venusaur, charmander, charmeleon, charizard,
                    squirtle, wartortle, blastoise, caterpie, metapod, butterfree, weedle, kakuna, beedrill, pidgey,
                    pidgeotto, pidgeot, rattata, raticate);

                    return pokemonsUrls;
                },

                
                goToNextVideo() {
                    this.currentVideoIndex++;
                    let pokemonsUrls = this.orderUrls();  
                    let singleVideo = pokemonsUrls[this.currentVideoIndex];
                    this.singleVideo = singleVideo; 
                },

                goToPreviousVideo(){
                    this.currentVideoIndex--; 
                    let pokemonsUrls = this.orderUrls();  
                    let singleVideo = pokemonsUrls[this.currentVideoIndex];
                    this.singleVideo = singleVideo; 
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
};


</style>
