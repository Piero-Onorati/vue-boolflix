<template>

    <div class="homepage">

        <!-- start cover-image -->
        <div class="cover-image" v-for="(item,index) in trending" :key="index" >

            <!-- IMAGE -->
            <img :src="'https://image.tmdb.org/t/p/original'+item.backdrop_path" alt="" v-if="index==counter" class="cover"> 

            <!-- NAME + BUTTON PLAY + BUTTON INFO -->
            <div class="info">
                <h1>{{item.original_name || item.original_title }}</h1>
                <button class="play"><i class="fas fa-play"></i><span>Riproduci</span></button>
                <button class="more-info"><i class="fas fa-info-circle"></i><span>Altre Info</span></button>
            </div> 

        </div>
        <!-- end cover-image -->

        <!-- start carousel container -->
        <div class="carousel-container">

            <!-- SECTION TITLE -->
            <h2>Trending today</h2>

            <!-- TRACK CONTAINING ALL THE CARDS -->
            <div class="track"> 
                <div class="card-container" v-for="(item,index) in trending" :key="index" @click="show(index)" >
                    <img :src="'https://image.tmdb.org/t/p/w342'+item.poster_path" alt="" >
                </div>
            </div>

            <!-- ARROW LEFT + ARROW RIGHT -->
            <div class="nav">
                <button class="left-arrow"  @click="prevSlide"><i class="fas fa-chevron-left"></i></button>
                <button class="right-arrow" @click="nextSlide"><i class="fas fa-chevron-right"></i></button>
            </div>
            <!-- end carousel container -->
        </div>

    </div>
    
</template>

<script>
import axios from 'axios'


export default {
    name:'HomePage',
    components:{
    },
    data(){
        return{
            trendingURL:'https://api.themoviedb.org/3/trending/all/day',
            myAPIKey:'d3cb662cdb093d83d0c5a79bf4d7718f',
            trending:[],
            counter:0
        }
    },

    created(){
        this.getTrending();
    },

    methods:{

        // AXIOS Call for generating the trending array
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

        },

        // Function for NEXT slider
        nextSlide: () => {

            let track = document.querySelector('.track');
          
            let carouselWidth = document.querySelector('.carousel-container').offsetWidth;

            track.style.transform=`translateX(-${carouselWidth}px)`

            window.addEventListener('resize', () => {
                carouselWidth = document.querySelector('.carousel-container').offsetWidth;
            })

        },

        // Function for PREV slider
        prevSlide:()=>{
            const track = document.querySelector('.track');

            track.style.transform=`translateX(${0}px)`
        },

        // Function to show the cover of the card in background
        show : function (index){
            this.counter = index
            console.log(this.counter);
            console.log('ciao')
        }

    }

}
</script>

<style lang="scss" scoped>

.homepage{
    height:100%;
    position: relative;
    overflow-x: auto;

    .cover-image{
        width: 100%;
        overflow: hidden;
        position: relative; 

        .info{
            font-size:24px ;
            line-height: 60px;
            width:600px;
            color: whitesmoke;
            text-shadow: 2px 2px black;
            position: absolute;
            left:30px;
            top:40%;

            button{
                font-size: 20px ;
                margin-top: 20px;
                padding: 12px 25px;
                outline: none;
                border:none;
                border-radius:5px;
                margin-right: 20px;

                &:hover{
                    filter: brightness(0.8);
                }

                span{
                   padding-left:18px
                }

            }
            .play{
                font-weight: bold ;
                background-color: #ffffff;
                color: #000000;
            }
            .more-info{
                background-color: #757576;
                color: white;
            }
        }

        .cover{
            width:100%;
            height: 650px;
            object-fit: cover;
            object-position: top;
        }
    }

    .carousel-container {
        width: 100%;
        margin: 0 auto;
        min-height: 300px;
        position: absolute;
        bottom:180px;
        left:0;
        position: relative;
        overflow: hidden;

        h2{
            font-size: 30px;
            color:white;
            text-shadow: 2px 2px rgb(48, 48, 48);
            margin:20px 0 5px 15px;
        }

        .track {
            display: inline-flex;
            transition: transform 0.5s;
    
            .card-container{
                width: calc(100% / 7 - 10px);
                flex-shrink: 0;
                height: 300px;
                margin: 0 5px;

                &:hover{
                    transform: scale(1.1);
                }   

                img{
                    width:100%;
                    height:100%;
                    border-radius:10px;
                }

            }

        }

        .nav{

            .left-arrow{
            background-color: white;
            width:50px;
            height: 50px;
            border-radius: 50% ;
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            left:0;
            opacity:0.3;

                &:hover{
                    opacity:1
                }

            }

            .right-arrow{
                background-color: white;
                width:50px;
                height: 50px;
                border-radius: 50% ;
                position: absolute;
                top: 50%;
                transform: translateY(-50%);
                right:1%;
                opacity:0.3;

                &:hover{
                    opacity:1
                }
            }

        }

    
    }

}



</style>