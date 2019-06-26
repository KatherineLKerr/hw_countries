<template lang="html">
  <div>
    <h1>countries:</h1>
    <div class="main-container">
      <!-- <countries-list :countries="countries"></countries-list> -->

      <select v-model="selectedCountry">
        <option v-for="(value, key) in countries" :value="value">{{value.name}}</option>
      </select>



      <country-detail :country="selectedCountry"></country-detail>
    </div>
  </div>
</template>

<script>
import CountriesList from './components/CountriesList.vue'
import CountryDetail from './components/CountryDetail.vue'
import { eventBus} from './main.js'

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null
    }//end of return
  },//end of data
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (country) => {
      this.selectedCountry = country
    })
  },//end of mounted
  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail
  }//end of component
}
</script>

<style lang="css" scoped>
</style>
