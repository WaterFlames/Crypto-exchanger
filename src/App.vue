<template>
  <h1>CRYPTO EXCHANGER</h1>

  <InputField :changeAmount="changeAmount" :convert="convert" :favourite="favourite"/>
  <p class="error" v-if="error !='' ">{{ error }}</p>
  <p class="result" v-if="result != 0 ">{{ result }}</p>
  <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>

  <div class="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond"/>
  </div>
</template>

<script>
import InputField from './components/InputField.vue';
import Selector from './components/Selector.vue';
import Favourite from './components/Favourite.vue';
// import Converter from './components/Converter.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

  export default {
    components: {InputField, Selector, Favourite},

    data(){
      return{
        amount: 0,
        cryptoFirst: '',
        cryptoSecond: '',
        error: '',
        result: 0,
        favs: [],
      };
    },

    methods:{
      changeAmount(val){
        this.amount = val
      },

      setCryptoFirst(val){
        this.cryptoFirst = val
      },
      setCryptoSecond(val){
        this.cryptoSecond = val
      },

      favourite(){
        this.favs.push({
          from: this.cryptoFirst,
          to: this.cryptoSecond,
        })
      },

      getFromFavs(index){
        this.cryptoFirst = this.favs[index].from
        this.cryptoSecond = this.favs[index].to
      },

      async convert(){
        this.result = 0;
        
        if(this.amount <= 0){
          this.error = "Enter a number greater than zero";
          return;
        } else if(this.cryptoFirst == '' || this.cryptoSecond == ''){
          this.error = "Select currency";
          return;
        } else if(this.cryptoFirst == this.cryptoSecond){
          this.error = "Select different currencies";
          return;
        }
        this.error = '';

        try {
          await convert.ready(); //Wait for the initial cache to load

          if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH') 
            this.result = convert.BTC.ETH(this.amount);
          else if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT') 
            this.result = convert.BTC.USDT(this.amount);
          else if(this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC') 
            this.result = convert.ETH.BTC(this.amount);
          else if(this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT') 
            this.result = convert.ETH.USDT(this.amount);
          else if(this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC') 
            this.result = convert.USDT.BTC(this.amount);
          else if(this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH') 
            this.result = convert.USDT.ETH(this.amount);
        } catch (error) {
          this.error = 'Conversion failed. Try again later.';
        }
      }
    }
  }
</script>

<style>
  .selectors{
    width: 700px;
    margin: 0 auto;
    display: flex;
    justify-content: space-around;
  }
</style>