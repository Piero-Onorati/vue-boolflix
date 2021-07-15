<template>

    <div class="card" v-if="details.poster_path !== null">
        
        <!-- IMG card -->
        <img  class="poster" :src="'https://image.tmdb.org/t/p/'+ size+details.poster_path">

        <!-- Card Description  -->
        <div class="card-description">

            <!-- Title of movie or TV-series -->
            <h5> {{details.title == null ? details.name :  details.title}}</h5>

            <!-- Original_Title of movie or TV-series -->
            <h6 >{{details.original_name || details.original_title }}</h6>

            <!-- start section info: click the button to show CAST AND GENRES -->
            <button class="info-button" @click="show"><i class="fas fa-info-circle"></i></button>
            <div class="info" v-if="active" >
                <!-- Cast -->
                <div class="info-col">
                    <h3>Cast:</h3>
                    <p v-for="actor in details.cast" :key="actor.id">{{actor.name}}</p>
                </div>

                <!-- genres -->
                <div class="info-col">
                    <h3>Genres:</h3>
                    <p v-for="genre in details.genre" :key="genre.id">{{genre.name}}</p>
                </div>
            </div>
             <!-- end section info: click the button to show CAST AND GENRES -->

            <!-- Original Language + flag-icon -->
            <h6 v-if="flagsCode.includes(details.original_language)">
                Language: <img  class="flag" :src="require(`../assets/flags/${details.original_language}.jpg`)">
            </h6>
            <h6 v-else>{{details.original_language}}</h6>

            <!-- Rating Stars -->
            <div class="stars-outer">
                <div class="stars-inner" :style="`width:${vote}%`"></div>
            </div>

            <!-- overview: plot description -->
            <p class="description">{{details.overview}}</p> 
            
        </div> 

    </div>
  
  
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
            active:false
        }
    },

    computed:{
        // function for converting the vote_average into a star rating system
        vote(){
            let starVote = this.details.vote_average * 5/10;
            let percentageVote = Math.round(starVote * 100/ 5);
            return percentageVote
        }
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

    &:hover{
        transform: scale(1.3);
        z-index: 5;
    }

    &:hover .card-description{
        display: block;
    }

    .poster{
        width:100%;
        height: 100%;
    }

    .card-description{
        padding:10px;
        width:100%;
        height: 100%;
        overflow-y:auto;
        position: absolute;
        top:50%;
        left: 50%;
        transform: translate(-50%,-50%);
        background-color: rgba(0, 0, 0, 0.466);
        color: white; 
        display: none;

        h6{
            margin: 3px 0 5px 0;
        }

        .info-button{
            font-size:20px;
            color: whitesmoke;
            background-color: transparent;
            border:none;
            outline:none
        }

        .info{
            display: flex;

            .info-col{
                font-size: 9px;
                color: lightgray;
                padding-left:7px ;

                h3{
                    color: white;
                }
                
            }
        }

    
        .flag{
            width:16px;
            height:10px;
        }
        

        .stars-outer{
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
        }

        .description{
            margin-top: 10px;
            width: 100%;
            font-size: 10px;
        }

    }
 
}



</style>