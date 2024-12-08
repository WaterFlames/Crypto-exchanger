<template>

</template>
  
<script>
  import CryptoConvert from 'crypto-convert';
  const convert = new CryptoConvert();
  
  export default {
    props: {
      amount: {
        type: Number,
        required: true,
      },
      cryptoFirst: {
        type: String,
        required: true,
      },
      cryptoSecond: {
        type: String,
        required: true,
      },
    },
    data() {
      return {
        error: '',
      };
    },
    methods: {
      async handleConversion() {
        if (this.amount <= 0) {
          this.error = 'Enter a number greater than zero';
          this.$emit('conversion-error', this.error);
          return;
        }
        if (!this.cryptoFirst || !this.cryptoSecond) {
          this.error = 'Select both currencies';
          this.$emit('conversion-error', this.error);
          return;
        }
        if (this.cryptoFirst === this.cryptoSecond) {
          this.error = 'Select different currencies';
          this.$emit('conversion-error', this.error);
          return;
        }
        this.error = '';
  
        try {
          await convert.ready(); // Дождаться загрузки кеша
          const conversionResult = convert[this.cryptoFirst][this.cryptoSecond](this.amount);
          this.$emit('conversion-success', conversionResult); // Отправка результата
        } catch (err) {
          this.error = 'Conversion failed';
          this.$emit('conversion-error', this.error);
        }
      },
    },
    watch: {
      // Автоматический пересчет при изменении входных данных
      amount: 'handleConversion',
      cryptoFirst: 'handleConversion',
      cryptoSecond: 'handleConversion',
    },
  };
</script>
  