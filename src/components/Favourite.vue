<template>
    <h2>Favourite list</h2>

    <!-- input 1-rts and 2-nd favourite -->
    <div @click="getFromFavs(index)" v-for="(el, index) in favs" :key="index">
        <span>{{ el.from }}</span>
        <span>{{ el.to }}</span>
    </div>
</template>
  
<script>
    export default{
        props:{
            favs:{
                type: Array,
                required: true
            },

            getFromFavs:{
                type: Function,
                required: true
            }
        }
    }
</script>
    
<style scoped>
    h2{
        color: #fff;
    }

    div{
        display: flex;
        justify-content: space-between;
        width: 500px;
        margin: 10px auto;
        transition: all 500ms ease;
    }

    div:hover{
        opacity: 0.7;
        transform: scale(1.1);
        cursor: pointer;
    }

    span{
        padding: 10px 15px;
        background: #8c00ff;
        color: #fff;
    }
</style>