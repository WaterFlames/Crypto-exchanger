<template>
  <h1>CRYPTO EXCHANGER</h1>
  <Input/>
  <div class="selectors">
    <Selector/>
    <Selector/>
  </div>
</template>

<script>
import InputField from './components/InputField.vue';
import Selector from './components/Selector.vue';
  export default {
    components: {InputField, Selector}
  };

</script>

<style>
  .selectors{
    width: 700px;
    margin: 0 auto;
    display: flex;
    justify-content: space-around;

  }
</style>