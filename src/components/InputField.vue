<template>
  <!-- input fields and convert and favourite btn-->
  <input type="number" placeholder="This field is waiting for your numbers" min="0" @input="changeAmount($event.target.value)"> <br>
  <button @click="convert()"> Convert </button>
  <button class="btn-fav" @click="favourite()"> Favourite </button>
</template>

  
<script>
  export default {
    props: {
      changeAmount: {
        type: Function,
        required: true,
      },
      convert: {
        type: Function,
        required: true,
      },
      favourite: {
        type: Function,
        required: true,
      },
    },

    methods: {
      handleConvert() {
         // calling a method from a prop
        this.convert();
      },
    },
  };
</script>
  
<style>
  input{
    width: 670px;
    padding: 10px 15px;
    border-radius: 3px;
    border: 0;
    font-size: 1.2em;
    background: #fafafa;
    color: #333;
    outline: none;
  }

  button{
    padding: 15px 20px;
    top: 10px;
    position: relative;
    text-transform: uppercase;
    cursor: pointer;
    background: #1a032d;
    color: #fff;
    border: 0;
    border-radius: 3px;
  }
</style>