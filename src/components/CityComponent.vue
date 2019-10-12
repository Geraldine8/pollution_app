<template lang="html">
  <div class="">
    <h3></h3>
    <select v-on:change="handleSelectedCountry">
      <option>Select</option>
      <option v-for="(country, index) in countries" :value="country.country">{{country.country}}</option>
    </select>

    <select v-on:change="handleSelectedState">
      <option>Select</option>
      <option v-for="(state, index) in states" :value="state.state">{{state.state}}</option>
    </select>

    <select v-on:change="handleSelectedCity">
      <option>Select</option>
      <option v-for="(city, index) in cities" :value="city.city">{{city.city}}</option>
    </select>
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

</style>

<!-- What is an Event Bus? Well, it’s kind of summed up in the name itself.
It’s a mode of transportation for one component to pass props from one
component to another, no matter where those components are located
in the tree.

EventBus allows us to emit an event in one component and
listen for that event in another. -->
