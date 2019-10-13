<template lang="html">
  <div class="">
    <h2>Air Quality App</h2>
    <div class="wrapper">
      <city-component :countries='countries' :states="states" :cities="cities"></city-component>
      <city-details :cityData='cityData'></city-details>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';
import CityComponent from './components/CityComponent.vue';
import CityDetails from './components/CityDetails.vue';

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      states: null,
      cities: null,
      pollution: null,
      key: '69e738aa-8b22-43a3-a8ad-d12b37ab1739',
      //key: 'c3dd44df-eff9-44b8-9f22-eb5fee8a4789',
      selectedCountry: '',
      selectedCity: '',
      cityData: null
      // newKey: 69e738aa-8b22-43a3-a8ad-d12b37ab1739
    };
  },

  mounted(){
    fetch(`https://api.airvisual.com/v2/countries?key=${this.key}`)
    .then(response => response.json())
    .then(apiResponse => this.countries = apiResponse.data)

    eventBus.$on('country-selected', (country) =>{
      this.selectedCountry = country;
      this.states = null
      fetch(`https://api.airvisual.com/v2/states?country=${country}&key=${this.key}`)
      .then(response => response.json())
      .then(apiResponse => this.states = apiResponse.data)
      this.cities = null
    })

    eventBus.$on('state-selected', (state) =>{
      if (state=='') {
        return;
      }
      this.selectedState = state;
      fetch(`https://api.airvisual.com/v2/cities?state=${state}&country=${this.selectedCountry}&key=${this.key}`)
      .then(response => response.json())
      .then(apiResponse => this.cities = apiResponse.data)
    })

    eventBus.$on('city-selected', (city) =>{
      if (city=='') {
        return;
      }
      this.selectedCity = city;
      fetch(`https://api.airvisual.com/v2/city?city=${city}&state=${this.selectedState}&country=${this.selectedCountry}&key=${this.key}`)
      .then(response => response.json())
      .then(apiResponse => this.cityData = apiResponse.data)
    })
  },

  components: {
    "city-component": CityComponent,
    "city-details": CityDetails




  }


}
</script>

<style lang="css" scoped>

h2 {
  text-align: center;
}


</style>
