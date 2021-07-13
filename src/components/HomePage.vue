<template>
<div>

    <section class="section-1">
    <h2>Trending today </h2>
    <div class="top-rated">
        <Card3 v-for="item in trending" :key="item.id" :details="item"/>
    </div>
    </section>

    <section class="section-1">
    <h2>Popular </h2>
    <div class="top-rated">
        <Card2  v-for="item in popular" :key="item.id" :details="item"/>
    </div>
    </section>

    

    <section class="section-1">
    <h2>Top rated Movies </h2>
    <div class="top-rated">
        <Card2  v-for="item in topRatedMovies" :key="item.id" :details="item"/>
    </div>
    </section>


</div>





  
</template>

<script>
import axios from 'axios'
import Card2 from '@/components/Card2.vue'
import Card3 from '@/components/Card2.vue'
export default {
    name:'HomePage',
    components:{
        Card2,
        Card3
    },
    data(){
        return{
            topRatedMovieURL:'https://api.themoviedb.org/3/movie/top_rated',
            popularURL:'https://api.themoviedb.org/3/movie/popular',
            trendingURL:'https://api.themoviedb.org/3/trending/all/day',
            myAPIKey:'d3cb662cdb093d83d0c5a79bf4d7718f',
            topRatedMovies:[],
            popular:[],
            trending:[]
        }
    },

    created(){
        this.topRatedMovie();
        this.getPopular();
        this.getTrending()
    },

    methods:{

        topRatedMovie(){
            axios
                .get(this.topRatedMovieURL, {
                    params:{
                        api_key:this.myAPIKey,
                        language: 'it-It'
                    }
                })
                .then(response=>
                    this.topRatedMovies=response.data.results
                )

        },

        getPopular(){
            axios
                .get(this.popularURL, {
                    params:{
                        api_key:this.myAPIKey,
                        language: 'it-It'
                    }
                })
                .then(response=>
                    
                     this.popular=response.data.results
                )

        },

        getTrending(){
            axios
                .get(this.trendingURL, {
                    params:{
                        api_key:this.myAPIKey,
                    }
                })
                .then(response=>
                    
                   this.trending=response.data.results
                )

        }

    }

}
</script>

<style lang="scss">

.section-1{
    padding-top:  120px;

    h2{
        color: whitesmoke;
    }

    .top-rated{
        display: flex;
    }

}


</style>