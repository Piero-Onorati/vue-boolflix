<template>

    <div class="container">
        <h3>Hai cercato: {{theSearch}}</h3>
        <div class="search-result">
            <Card v-for="movie in arrayMovie" :key="movie.id" :details="movie"  />
            <Card v-for="serie in arraySerie" :key="serie.id" :details="serie"  />
        </div>
    </div>
  
</template>

<script>

import Card from '@/components/Card.vue'


export default {
    name:'MainContent',
    components:{
        Card,
    },
    props:{
        arrayMovie: Array,
        arraySerie: Array,
        theSearch: String
    }

}
</script>

<style lang="scss" scoped>

.container{

    h3{
        padding-top:100px;
        padding-left: 30px;
        color: lightgray;
    }

    .search-result{
        padding: 20px 20px 50px 20px;
        display: flex;
        flex-flow: row wrap;
    }

}




</style>