<template>
  <nav>
      <ul class="navbar">
        <li v-for="(link,index) in navBar" :key="index">
            <a href="#" :class="{ active: link.selected }">{{link.linkName}}</a>
        </li>
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
                    selected: true
                },
                {
                    linkName:'Serie TV',
                    selected: false
                },
                {
                    linkName:'Film',
                    selected: false},
                {
                    linkName:'Nuovi e Popolari',
                    selected: false
                },
                {
                    linkName:'La mia lista',
                    selected: false
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
        font-size:15px;

        a{
            color: lightgray;
            text-decoration: none;

            &.active{
                color:white;
                font-weight: bold;
            }
        }
        
    }
}

</style>