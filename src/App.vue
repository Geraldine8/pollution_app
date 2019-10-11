<template lang="html">
  <div class="">
    <h2>Air Quality App</h2>
    <div class="wrapper">
      <air-countries :countries='countries'></air-countries>

    </div>

  </div>
</template>

<script>
import {eventBus} from './main.js';
import AirCountries from './components/AirCountries.vue';
import AirCountriesName from './components/AirCountriesName.vue';

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      cities: [],
      pollution: null

    };
  },
  mounted(){
    fetch('http://api.airvisual.com/v2/countries?key=c3dd44df-eff9-44b8-9f22-eb5fee8a4789')
    .then(response => response.json())
    .then(countries => this.countries = countries)

    // eventBus.$on('country-selected', (country) =>{
    //   this.seelectedCountry = country;
    // })


  },

  components: {
    "air-countries": AirCountries,
    "air-countries-name": AirCountriesName

  }


}
</script>

<style lang="css" scoped>
</style>
