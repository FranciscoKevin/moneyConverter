<template>
  <div id="app">
  <h1>Money Converter Euros/Dollars</h1>
  <p>
    EUR(€) to change in USD($) :
    <input v-model="euros">
  </p>
  <p>{{ conversion }}</p>
</div>
</template>

<script>
import * as _ from 'lodash'

export default {
  name: 'MoneyConverter',
  data: function() {
    return {
      euros: '',
      taux: '',
      conversion: ''
    }
  },
   methods: {
    getConversion: _.debounce(function () {
      if (!this.euros) {
        this.conversion = "I can't give you an answer until you enter a number!";
        return;
      } else if (this.euros.search(/^[\d.,]+$/) === -1) {
        this.conversion = 'Enter only numbers please'
        return
      }
      this.$http
        .get('https://open.er-api.com/v6/latest/EUR')
        .then(function (response) {
          this.taux = response.body.rates.USD;
          this.conversion = `${(
            this.taux * this.euros.replace(',', '.')
          ).toFixed(2)} $`;
        })
        .catch(function (error) {
          this.conversion = "Error ! Unable to access the API." + error
        })
    }, 500)
  },
  watch: {
    euros: function () {
      this.getConversion()
    }
  }
}
</script>

<style scoped>

</style>
