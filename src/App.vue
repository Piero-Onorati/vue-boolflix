<template>
  <div id="app">
    <Header @search="receivedInput" />
    <HomePage v-if="inputText ==''"/>
    <MainContent v-else :arrayMovie="movies" :arraySerie="series" :theSearch="inputText"/>
  </div>
</template>

<script>
import axios from 'axios'
import Header from './components/Header.vue'
import HomePage from './components/HomePage.vue'
import MainContent from './components/MainContent.vue'

export default {
  name: 'App',
  components: {
    Header,
    HomePage,
    MainContent
  },
  data(){
    return{
      movieURL:'https://api.themoviedb.org/3/search/movie',
      movieDetail:'https://api.themoviedb.org/3/movie',
      serieURL:'https://api.themoviedb.org/3/search/tv',
      myAPIKey:'d3cb662cdb093d83d0c5a79bf4d7718f',
      inputText:'',
      movies:[],
      series:[],
    }
  },

  methods:{
    readTheAPI(input){
      axios
        .get(this.movieURL,{ 
          params: {
            api_key:this.myAPIKey,
            query: input,
            language: 'it-It',
          }})
        .then( response =>{
          this.movies = response.data.results;

            // add Cast to each element
            this.movies.forEach(element => {
              axios
              .get(`https://api.themoviedb.org/3/movie/${element.id}/credits`,{
                params:{
                  api_key:this.myAPIKey,
                }})
              .then(response=>{
                element.cast= response.data.cast.slice(0, 5)
              })
              
            });

            // add Genre to each element
            this.movies.forEach(element => {
              axios
              .get(`https://api.themoviedb.org/3/movie/${element.id}`,{
                params:{
                  api_key:this.myAPIKey,
                  append_to_response:'details'
                }})
              .then(response=>{
                element.genre= response.data.genres
              })
              
            });
            console.log(this.movies);
          
        })
        .catch(error =>{
          console.log('Errore', error);
      });


      axios
        .get(this.serieURL,{
          params: {
            api_key: this.myAPIKey,
            query: input,
            language: 'it-It'
          }

        })
        .then( response =>{
          this.series=response.data.results;

            // add Cast to each element
            this.series.forEach(element => {
              axios
              .get(`https://api.themoviedb.org/3/tv/${element.id}/credits`,{
                params:{
                  api_key:this.myAPIKey,
                }})
              .then(response=>{
                element.cast= response.data.cast.slice(0, 5)
              })
              
            });

            // add Genre to each element
            this.series.forEach(element => {
              axios
              .get(`https://api.themoviedb.org/3/movie/${element.id}`,{
                params:{
                  api_key:this.myAPIKey,
                  append_to_response:'details'
                }})
              .then(response=>{
                element.genre= response.data.genres
              })
              
            });
            console.log(this.series);
        })
        .catch(error =>{
          console.log('Errore', error);
        })

    },


    receivedInput(arg){
      this.inputText = arg;
      this.readTheAPI(arg);
    }

  }
}
</script>

<style lang="scss">
@import '@/style/commons.scss'; 

#app{
  background-color: black;
  height: 100vh;
  overflow-x: auto;
}


</style>
