<template>
<div class="header">
    <div class="container">
        <div class="left-header">
            <img src="../assets/img/netflix-logo.png" alt="">
            <Menu/>
        </div>

        <div class="right-header">
            <div class="search-box">
                <input v-if="active" type="text" placeholder="Search..." class="search-input" v-model.trim="searchMovie"  @keyup.enter="searchAndReset"> 
                <button @click="toggleSearch" class="search-btn">
                    <i class="fas fa-search "></i>
                </button>
            </div>
            <i class="fas fa-bell"></i>
            <img src="../assets/img/user-profile.png" alt="">
        </div>
    </div>
</div>
  
</template>

<script>
import Menu from '@/components/Menu.vue'
export default {
    name:'Header',
    components:{
        Menu

    },
    data(){
        return{
            searchMovie:'',
            active: false
        }
    },
    methods:{
        searchAndReset(){
            this.$emit('search',this.searchMovie);    
            this.searchMovie =''        
        },

        //toggle for dropdown menu of each message
        toggleSearch(){
            this.active = !this.active;
        },

    }

}
</script>

<style lang="scss">

.header{
    position:fixed;
    z-index: 1;
    width: 100%;
    padding: 20px 0;
    background-image: linear-gradient(#000, rgba(0, 0, 0, 0.158));

    .container{
        color:white;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .left-header{
            display: flex;

            img{
            width: 110px
            }
        }

        .right-header{
            display: flex;
            align-items: center;
            font-size:22px ;

            .search-box{
                margin: 0 30px;
                display: flex;

                .search-input {
                    margin-right: 10px;
                    padding:5px 10px;
                    background: none;
                    outline: none;
                    color: white;
                    transition: 0.4s;
                    border: 1px solid white;
                }

                .search-btn {
                    outline:none;
                    border: none;
                    background-color: transparent;
                    color: white;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    transition: 2s;
                    font-size: 22px;

                }

            }

            img{
                margin-left: 30px ;
                width:40px
            }

        }
    
    }
}


</style>