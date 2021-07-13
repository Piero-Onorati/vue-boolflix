<template>
<div>
    <img  class="poster" :src="'https://image.tmdb.org/t/p/w342'+details.poster_path" alt="">
</div>
  
  
</template>

<script>
export default {
    props:{
        details:Object
    }

}
</script>

<style>

</style>