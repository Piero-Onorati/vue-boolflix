<template>
  <section>
    <!-- SECTION TITLE -->
    <h2>Popular TV series</h2>

    <!-- Carousel -->
    <carousel :per-page="6" :mouse-drag="true">   
        <slide  class="slide" v-for="(el,index) in arrayPopularTv" :key="index" >
            <img :src="'https://image.tmdb.org/t/p/w342'+el.backdrop_path" :alt="el.name"> 
        </slide>
    </carousel>
  </section>
</template>

<script>
import { Carousel, Slide } from 'vue-carousel';

export default {
    name:'PopularTV',
    props:{
        arrayPopularTv:Array
    },
    components:{
        Carousel,
        Slide
        
    },
    data(){
        return{
            showVid:false
        }
    }

}
</script>

<style lang="scss" scoped>

section{
    padding-bottom: 30px;

    h2{
        font-size: 30px;
        color:white;
        text-shadow: 2px 2px rgb(48, 48, 48);
        margin:20px 0 10px 25px;
    }
    
    img{
        padding-right: 8px;
        border-radius: 20px;
    
        &:hover{
            transform: scale(1.03);
        }
    }

}


</style>