<template>
    <div>
        <Search @search="receivedMovieName"/>
        <Card :details="movie" v-for="movie in movies" :key="movie.id"/>
    </div>
  
</template>

<script>
import axios from 'axios'
import Card from '@/components/Card.vue'
import Search from '@/components/Search.vue'

export default {
    name:'MainContent',
    components:{
        Card,
        Search
    },
    data(){
        return{
            movieURL:'https://api.themoviedb.org/3/search/movie',
            myAPIKey:'d3cb662cdb093d83d0c5a79bf4d7718f',
            movieName:'',
            movies:[]
        }
    },
    
    computed:{
        filteredMovie(){
            return this.movie.filter(element=>{
                if (element.title.toLowerCase().includes(this.movieName.toLowerCase()) ||
                    element.original_title.toLowerCase().includes(this.movieName.toLowerCase())) {
                        return element
                    
                }
            })
        }
    },

    created(){
        this.receivedMovieName()
    },

    methods:{
        readTheAPI(){
            axios
                .get(this.movieURL,{ 
                    params: {
                        api_key:this.myAPIKey,
                        query: this.movieName,
                        language: 'it-It'
                    }}
                   )
                .then( response =>{
                    this.movies = response.data.results
                    console.log(response);
                })
                .catch(error =>{
                    console.log('Errore', error);
                })

        },

        receivedMovieName(arg1){
            this.movieName = arg1
            this.readTheAPI()
        }

    }

}
</script>

<style>

</style>