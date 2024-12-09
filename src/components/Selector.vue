<template>
    <ul>
        <li @click="selectItem('BTC')" :class="{ active: current === 'BTC' }"> Bitcoin </li>
        <li @click="selectItem('ETH')" :class="{ active: current === 'ETH' }"> ETH </li>
        <li @click="selectItem('USDT')" :class="{ active: current === 'USDT' }"> USDT </li>
    </ul>
</template>
  
<script>
  export default {
    props:{
        setCrypto:{
            type: Function,
            required: true
        }
    },

    data(){
        return{
            current: ''
        }
    },

    methods: {
        selectItem(val) {
            this.setCrypto(val);
            this.current = val;
        },
    }
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