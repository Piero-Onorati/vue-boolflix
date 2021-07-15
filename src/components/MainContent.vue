<template>

    <div class="container">

        <!-- start top-part -->
        <div class="top-part">
            <h3>Hai cercato: {{theSearch}}</h3>
            <div class="select">
                <h5>Sort by genre</h5>
                <select v-model="selecting" @change="selectGenre">
                    <option v-for="(option,index) in allGenres" :key="index" >{{option}}</option>
                </select>
            </div>
        </div>
        <!-- end top-part -->

        <!-- start search-result -->
        <div class="search-result">
            <Card v-for="item in series" :key="item.id" :details="item" />
            <Card v-for="item in movies" :key="item.id" :details="item" />
        </div>
        <!-- end search-result -->
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
        series: Array,
        movies:Array,
        theSearch: String,
        allGenres:Array
    },
    data(){
        return{
            selecting: ''
        }
    },

    created(){
        this.selectGenre()

    },
    methods:{
        selectGenre(){
            console.log(this.selecting)
            this.$emit('vModelGenre', this.selecting)
        }
    }

}
</script>

<style lang="scss" scoped>

.container{

    .top-part{
        height: 50px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top:100px ;

        h3{
            color: lightgray;
        }
        .select{
            display: flex;
            align-items: center;

            h5{
                color: lightgray;
                margin-right: 10px;
            }
        }
    }
    
    .search-result{
        padding: 20px 20px 50px 20px;
        display: flex;
        flex-flow: row wrap;
    }

}


</style>