<template lang="html">
  <div class="">
    <h3></h3>
    <span>
      <air-countries-name v-for="(country, index) in countries" :country="country" :key="index" ></air-countries-name>
    </span>
  </div>
</template>

<script>
import AirCountriesName from './AirCountriesName.vue'

export default {
  name:'air-countries',
  props: ['countries'],
  components:{
    "air-countries-name": AirCountriesName
  }
}
</script>

<style lang="css" scoped>

</style>
