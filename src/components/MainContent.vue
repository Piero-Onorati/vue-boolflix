<template>

    <div class="container">
        <div class="search-result">
            <Card v-for="(item,index) in list" :key="index" :details="item"  />
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
    min-height: 100vh;
    padding: 120px 20px 50px 20px;
    display: flex;
    flex-flow: row wrap;
}

</style>