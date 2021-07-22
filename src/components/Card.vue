<template>
<section>
    <div class="card" v-if="details.poster_path !== null">     
        <!-- IMG card -->
        <img  class="poster" :src="'https://image.tmdb.org/t/p/'+ size+details.poster_path">

        <div class="show-info">
            <button @click="showModal = true"><i class="fas fa-info-circle info"></i>Show detail</button>
        </div>

    </div>

    <!-- Card Description  -->
    <div class="card-description" v-if="showModal">

        <!-- close button -->
        <button class="close-card" @click="showModal = false"><i class="fas fa-times"></i></button>

        <!-- backdrop_path image -->
        <div class="backdrop_path" v-if="details.backdrop_path != null">
            <img :src="'https://image.tmdb.org/t/p/original/'+ details.backdrop_path">
        </div>
        <div class="backdrop_path" v-else>
            <img class="alternative-image" :src="'https://image.tmdb.org/t/p/w500/'+ details.poster_path">
        </div>

        <!-- text card -->
        <div class="text">

            <div class="heading">
                
                <div class="left-col">

                    <!-- Title of movie or TV-series -->
                    <h5 class="title"> {{details.title == null ? details.name :  details.title}}</h5>

                    <!-- Original_Title of movie or TV-series -->
                    <h6 class="subtitle" >{{details.original_name || details.original_title }}</h6>

                    <!-- Original Language + flag-icon -->
                    <span v-if="flagsCode.includes(details.original_language)">
                        Language: <img  class="flag" :src="require(`../assets/flags/${details.original_language}.jpg`)">
                    </span>
                    <span v-else>{{details.original_language}}</span>

                    <!-- Rating Stars -->
                    <!-- (questo primo metodo richiede funzione in COMPUTED) -->
                    <!-- <div class="stars-outer">
                        <div class="stars-inner" :style="`width:${vote}%`"></div>
                    </div> -->
                    <div class="stars">
                        <span v-for="(start,index) in Math.ceil(details.vote_average/2)" :key="index" >
                            <i class="fas fa-star"></i>
                            </span>
                        <span v-for="(start,index) in 5 - Math.ceil(details.vote_average/2)" :key="'a'+ index" >
                            <i class="far fa-star"></i>
                        </span>
                    </div>

                </div>

                <div class="rigth-col">
                    <!-- start section info: click the button to show CAST AND GENRES -->
                    <!-- <button class="info-button" @click="show"><i class="fas fa-plus-circle"></i><span>More Info</span></button> --> 
                    <!-- (devi aggiunge v-if="active" al div "info" se riattivi il button sovrastante) -->
                    <div class="info">
                        <!-- Cast -->
                        <div class="info-col">
                            <h3>Cast:</h3>
                            <div class="cast">
                                <span v-for="actor in details.cast" :key="actor.id">&bull; {{actor.name}} </span>
                            </div>
                        </div>

                        <!-- genres -->
                        <div class="info-col">
                            <h3>Genres:</h3>
                            <div class="genres">
                                <span v-for="genre in details.genre" :key="genre.id">&bull; {{genre}} </span>
                            </div>
                        </div>
                    </div>
                     <!-- end section info: click the button to show CAST AND GENRES -->

                </div>

            </div>

            <!-- overview: plot description -->
            <p class="description">{{details.overview}}</p> 

        </div>

        
    </div> 

    <div class="background-overlay" v-if="showModal"></div>

</section>
  
  
</template>

<script>

export default {
    name:'Card',
    props:{
        details: Object
    },
    data(){
        return{
            size:'w342',
            flagsCode:["en", "it", "es", "fr", "ja", "de"],
            active:false,
            showModal :false,
        }
    },

    computed:{
        // function for converting the vote_average into a star rating system
        // vote(){
        //     let starVote = this.details.vote_average * 5/10;
        //     let percentageVote = Math.round(starVote * 100/ 5);
        //     return percentageVote
        // }
    },


    methods:{
        // function for show the info:cast + genres
        show(){
            this.active=!this.active
        }
    }

    
}
</script>

<style lang="scss" scoped>

.card{
    width:190px;
    height: 290px;
    margin: 12px 5px;
    background-color: #333333;
    border-radius:5px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    position: relative;

    &:hover{
        transform: scale(1.3);
        z-index: 5;
    }

    &:hover .show-info{
        display: flex;
    }

    .poster{
        width:100%;
        height: 100%;
    }
    .show-info{
        display: none;
        align-items: center;
        justify-content: center;
        position:absolute;
        bottom:0;
        left:0;
        width: 100%;
        height: 50px;
        background:rgba(44,44,44, 0.8);
        

        button{
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            background-color: transparent;
            border: none;
            .info{
                margin-right: 10px;
                font-size: 24px;
            }

            &:hover{
                color: lightgrey;
            }
       
        }
    }


    
}

.card-description{
    width:700px;
    height: 700px;
    position: fixed;
    top:30px;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 10px;
    overflow: hidden;
    background-color: #181818;
    color: white; 
    z-index: 9;

    .close-card{
        position:absolute ;
        top:20px;
        right: 20px;
        width: 40px;
        height: 40px;
        font-size: 20px;
        font-weight: 300;
        border: 1px solid white;
        border-radius: 50%;
        z-index: 10;
        color: white;
        background-color: rgba(0,0,0, 0.5);
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .backdrop_path{
        height: 400px;
        width: 100%;
        position: relative;
        overflow: hidden;

       
        img{
            width: 100%;
        }

        .alternative-image{
            object-fit: cover;
            object-position: center;
        }
    }

    .text{
        height: calc(100% - 400px);
        overflow-y: auto;

        .heading{
            padding: 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
    
            .left-col{
                .title{
                font-size:24px ;
                }
                .subtitle{
                    font-size: 15px;
                    font-weight: 300;
                    font-style: italic;
                    color: lightgrey;
                }

                span{
                    font-weight: 300;
                    margin: 10px 0 5px 0;
                }

                /* .info-button{
                    font-size:16px;
                    color: whitesmoke;
                    background-color: rgba(128, 128, 128, 0.527);
                    border:1px solid white;
                    border-radius: 5px;
                    outline:none;
                    display: flex;
                    align-items: center;
                    padding: 3px 5px;
                    margin-bottom:5px;

                    span{
                        font-size:10px ;
                        margin-left:5px;
                    }
                } */

                .flag{
                    width:16px;
                    height:10px;
                }
            
                /* .stars-outer{

                    /* css per il primo metodo, quello che richiede COMPUTED

                    display: inline-block;
                    position:relative;


                    .stars-inner{
                        position: absolute;
                        top: 0;
                        left:0;
                        white-space: nowrap;
                        overflow: hidden;  
                    } 

                    .stars-inner::before{
                        font-family: "Font Awesome 5 Free";
                        content:"\f005 \f005 \f005 \f005 \f005";
                        font-weight: 900;
                        color:yellow;
                    }

                } 

                .stars-outer::before{
                    font-family: "Font Awesome 5 Free";
                    content:"\f005 \f005 \f005 \f005 \f005";
                    font-weight: 200;
                } */
            }
    
            .rigth-col{
                width:40%;
                height: 100%;

                .info{
                    display: flex;
                    flex-direction: column;

                    .info-col{
                        font-size: 12px;
                        color: lightgray;
                        padding-left:7px;

                        h3{
                            color: white;
                        }

                        
                    }

                }
            }
    
        }

    }

    .description{
        padding: 10px 20px;
        width: 100%;
        font-size: 14px;
    }

}

.background-overlay{
    position: fixed;
    top:0;
    left:0;
    bottom:0;
    right: 0;
    transition: 200ms ease-in-out;
    background-color: rgba(0,0,0, 0.5);
    pointer-events: none;
    z-index: 1;
}
 



</style>