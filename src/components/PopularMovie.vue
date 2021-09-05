<template>
    <section>
      <!-- SECTION TITLE -->
    <h2>Popular Movie</h2>

    <div class="wrapper">

      <!-- Carousel -->
      <agile :key="popularMovie.length" :slidesToShow="5" :dots="false" :infinite="false"  :navButtons="false" ref="carousel">
        <div class="slide" v-for="(el,index) in popularMovie" :key="index">

          <!-- IMG -->
          <img :src="'https://image.tmdb.org/t/p/w342'+el.backdrop_path" :alt="el.title">   
          <!-- Card Body -->
          <div class="card-body">

            <!-- ICONS -->
            <div class="card-icons">
              <div class="icons-container">
                <div class="circle-icon"><i class="fas fa-play"></i></div>
                <div class="circle-icon"><i class="far fa-thumbs-up"></i></div>
                <div class="circle-icon"><i class="far fa-thumbs-down"></i></div>
              </div>
              <div class="circle-icon"><i class="fas fa-chevron-down"></i></div>
            </div>
            <!-- Movies name -->
            <h4>{{el.title}}</h4>

          </div> 

        </div>
      </agile>

      <!-- LEFT button -->
      <button class="btn btn_prev" @click="$refs.carousel.goToPrev()"><i class="fas fa-chevron-left"></i></button>
      <!-- RIGHT button -->
      <button class="btn btn_next" @click="$refs.carousel.goToNext()"><i class="fas fa-chevron-right"></i></button> 

    </div>
  
  </section>
</template>

<script>
import { VueAgile } from 'vue-agile'
export default {
    name:'PopularMovie',
    props:{
      popularMovie:Array
    },
    components:{
      agile: VueAgile 
    },
    data(){
      return{
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
        margin:0px 0 10px 25px;
    }

    .wrapper{
        position: relative;

        .agile{

            .slide{
                position: relative;
                height: 255px;

                img{
                    width:100%;
        
                &:hover{
                    cursor: pointer;
                }
        
                }

                .card-body{
                    color: honeydew;
                    background: #141414;
                    overflow: hidden;
                    height: 0;
                    padding: 0 10px;

                    h4{
                        padding: 10px;
                    }

                    .card-icons{
                        width: 100%;
                        display: flex;
                        align-items: center;
                        justify-content: space-between;

                        .icons-container{
                            display: flex;
                            align-items: center;
                        }

                        .circle-icon{
                            width:35px;
                            height: 35px;
                            font-size:13px;
                            border-radius: 50%;
                            background: #242424;
                            border:2px solid lightgrey;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            margin: 0 5px;

                            &:hover{
                                cursor:pointer;
                                background: #2e2e2e;
                                border:2px solid darkgrey;
                                color: lightgray;
                            }
                        }
                    }
                }

                &:hover{
                    background: #141414;
                }

                &:hover .card-body{
                    height: 100%;
                }
            }
        }

        .btn{
            background-color: white;
            width:50px;
            height: 50px;
            border-radius: 50% ;
            position: absolute;
            top: 30%;
            right:1%;
            opacity:0.6;

            &:hover{
                cursor: pointer;
                opacity:1
            }
            
        }

        .btn_prev{
            left:0
        }

        .btn_next{
            right: 0;
        }


    }
}

</style>