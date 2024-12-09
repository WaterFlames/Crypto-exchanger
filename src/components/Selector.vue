<template>
    <!-- current == 'BTC' ? 'active' :'' -->
    <ul> 
        <li @click="setCrypto('BTC')" :class="cryptoNow == 'BTC' ? 'active' :''"> Bitcoin </li>
        <li @click="setCrypto('ETH')" :class="cryptoNow == 'ETH' ? 'active' :''"> ETH </li>
        <li @click="setCrypto('USDT')" :class="cryptoNow == 'USDT' ? 'active' :''"> USDT </li>
    </ul>
</template>
  
<script>
  export default {
    props:{
        setCrypto:{
            type: Function,
            required: true
        },
        cryptoNow:{
            type: String,
            required: true
        }
    },
 };
</script>
  
<style>
    ul{
        width: 200px;
        padding: 0;
        list-style: none;
        border-radius: 3px;
        border: 3px solid #000;
    }

    li{
        display: block;
        background: #1A032D;
        color: #fff;
        padding: 20px 0;
    }

    li:hover{
        background: #0e0118;
        cursor: pointer;
    }
    .active{
        background: #0e0118;
    }
</style>