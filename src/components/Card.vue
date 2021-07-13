<template>

    <div class="card">
        <img :src="'https://image.tmdb.org/t/p/'+ size+details.poster_path" alt="">
        <p>{{details.title}}-{{details.name}}</p>
    </div>
  
</template>

<script>
export default {
    name:'Card',
    props:{
        details: Object,
        language:String,
        vote:Number
    },
    data(){
        return{
            size:'w342'
        }
    }


}
</script>

<style lang="scss">

.card{
    width:190px;
    height: 290px;
    margin: 10px 5px;
    background-color: #333333;
    border-radius:5px;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;

    &:hover{
        transform: scale(1.1);
    }

    img{
        width:100%;
        height: 100%;
        position: absolute;
        top:50%;
        left: 50%;
        transform: translate(-50%,-50%);
    }

    p{
         position: absolute;
        top:50%;
        left: 50%;
        transform: translate(-50%,-50%);
        background-color: rgba(0, 0, 0, 0.493);

    }


}



</style>