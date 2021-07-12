<template>
    <div>
        <input type="text" v-model.trim="searchMovie">
        <button @click="searchAndReset">click me!</button>
        
    </div>
  
</template>

<script>
export default {
    name:'Search',
    data(){
        return{
            searchMovie:''
        }
    },
    methods:{
        searchAndReset(){
            this.$emit('search',this.searchMovie);    
            this.searchMovie =''        
        }

    }

     

}
</script>

<style>

</style>