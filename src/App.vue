<template>
  <div id="app">
    <Header @search="receivedInput" />
    <HomePage v-if="inputText ==''"/>
    <MainContent v-else :list="finalList" :theSearch="inputText"/>
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
      series:[]
    }
  },
    
  computed:{
    finalList(){  
      let arr1=this.movies
      let arr2= this.series
      return [...arr1,...arr2] 
    }
  },

  methods:{
    readTheAPIMovie(input){
      axios
        .get(this.movieURL,{ 
          params: {
            api_key:this.myAPIKey,
            query: input,
            language: 'it-It',
          }})
        .then( response =>{
          this.movies = response.data.results
        })
        .catch(error =>{
          console.log('Errore', error);
      });

    },

    readTheAPISerie(input){
      axios
        .get(this.serieURL,{
          params: {
            api_key: this.myAPIKey,
            query: input,
            language: 'it-It'
          }

        })
        .then( response =>{
          this.series=response.data.results
        })
        .catch(error =>{
          console.log('Errore', error);
        })

    },

    receivedInput(arg){
      this.inputText = arg;
      this.readTheAPIMovie(arg);
      this.readTheAPISerie(arg)
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
