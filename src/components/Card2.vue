<template>

<div>
    <img  class="poster" :src="'https://image.tmdb.org/t/p/w342'+details.backdrop_path" alt="">
</div>
  
</template>

<script>
export default {
    props:{
        details:Object
    }

}
</script>

<style lang="scss">
    

</style>