<template>

    <div class="card" v-if="details.poster_path !== null">
        
        <img  class="poster" :src="'https://image.tmdb.org/t/p/'+ size+details.poster_path" alt="">
        <div class="card-description">
        
            <h5 v-if="details.title == null"> {{details.name}}</h5>
            <h5 >{{details.title}}</h5>

            <h6 v-if="details.original_name == null">{{details.original_name}}</h6>
            <h6> {{details.original_title}}</h6>

            <h6>Language: <img  class="flag" :src="require('../assets/flags/'+ details.original_language+'.jpg')"></h6>

            <div class="stars-outer">
                <div class="stars-inner" :style="`width:${vote}%`"></div>
            </div>

            <!-- <img :src="'https://image.tmdb.org/t/p/w500'+details.backdrop_path"> -->

            <p class="description">{{details.overview}}</p>
            
            
        </div>
        
    </div>
  
</template>

<script>
export default {
    name:'Card',
    props:{
        details: Object,
    },
    data(){
        return{
            size:'w342',
            
            
        }
    },
    computed:{
        vote(){
            let starVote = this.details.vote_average * 5/10;
            let percentageVote = starVote * 100/ 5;
            return percentageVote
        }

        // flag(){}
    },

    

  
        
    
}
</script>

<style lang="scss">

.card{
    width:190px;
    height: 290px;
    margin: 12px 5px;
    background-color: #333333;
    border-radius:5px;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;

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
        position: absolute;
        top:50%;
        left: 50%;
        transform: translate(-50%,-50%);
    }

    .card-description{
        width:100%;
        height: 100%;
        position: absolute;
        top:50%;
        left: 50%;
        transform: translate(-50%,-50%);
        background-color: rgba(0, 0, 0, 0.664);
        color: white;
        display: none;

   

        .flag{
            width:20px;
            height:10px;
        }


        

        .description{
            font-size: 10px;
            overflow: hidden;
            text-overflow: ellipsis;
            width:180px;
            height: 100px;
        }

        .stars-outer{
            display: inline-block;
            position:relative
        }


        .stars-outer::before{
            font-family: "Font Awesome 5 Free";
            content:"\f005 \f005 \f005 \f005 \f005";
            font-weight: 200;
        }

        .stars-inner{
            position: absolute;
            top: 0;
            left:0;
            white-space: nowrap;
            overflow: hidden;
            /* width: 0; */
    
           
        } 
 
        .stars-inner::before{
            font-family: "Font Awesome 5 Free";
            content:"\f005 \f005 \f005 \f005 \f005";
            font-weight: 900;
            color:yellow;
             
            
        } 
    }

   


}



</style>