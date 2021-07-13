<template>
    <div class="container">
        <div class="search-result">
            <Card  v-for="item in list" :key="item.id"
            :details="item"
            :language="item.original_language"
            :vote="item.vote_average"/>
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
        list: Array
    }
    
    

}
</script>

<style lang="scss">

.search-result{
    display: flex;
    flex-flow: row wrap;
    justify-content: center;

}

</style>