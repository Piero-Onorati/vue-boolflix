<template>
  <nav>
      <ul class="navbar">
          <li v-for="(link,index) in navBar" :key="index">{{link.linkName}}<a href="#"></a></li>
      </ul>
  </nav>
</template>

<script>
export default {
    name: 'Menu',
    data(){
        return{
            navBar:[
                {
                    linkName:'Menu',
                    active: true
                },
                {
                    linkName:'Serie TV',
                    active: false
                },
                {
                    linkName:'Film',
                    active: false},
                {
                    linkName:'Nuovi e Popolari',
                    active: false
                },
                {
                    linkName:'La mia lista',
                    active: false
                }
            ]
        }
    }

}
</script>

<style lang="scss">

.navbar{
    display:flex;
    margin-left: 30px;

    li{
        list-style: none;
        margin: 0 10px;

    }
}

</style>