<template lang="html">
  <div>
    <h3></h3>
    <div class="select">
      <select v-on:change="handleSelectedCountry">
        <option value="">Select Country</option>
        <option value="UK">United Kingdom</option>
        <option v-for="(country, index) in countries" :value="country.country">{{country.country}}</option>
      </select>

      <select v-if="states" v-on:change="handleSelectedState">
        <option value="">Select State</option>
        <option v-for="(state, index) in states" :value="state.state">{{state.state}}</option>
      </select>

      <select v-if="cities" v-on:change="handleSelectedCity">
        <option value="">Select City</option>
        <option v-for="(city, index) in cities" :value="city.city">{{city.city}}</option>
      </select>

    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name:'city-component',
  props: ['countries', 'states', 'cities'],
  methods: {
    handleSelectedCountry(event){
      eventBus.$emit('country-selected', event.target.value)
    },

    handleSelectedState(event){
      eventBus.$emit('state-selected', event.target.value)
    },

    handleSelectedCity(event){
      eventBus.$emit('city-selected', event.target.value)
    },
  }

}
</script>

<style lang="css" scoped>

.select {
  text-align: center;
  padding-bottom: 30px;
}
</style>



<!-- EventBus allows us to emit an event in one component and
listen for that event in another. -->
