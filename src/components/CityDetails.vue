<template lang="html">
  <div v-if='cityData'>
    <p>Weather: {{cityData.current.weather.tp }} °C </p>
    <p>Humidity: {{cityData.current.weather.hu}} % </p>
    <p>Pressure: {{cityData.current.weather.pr}} hPa</p>
    <p>Wind Speed: {{cityData.current.weather.ws}} m/s</p>
    <img :src="`images/${cityData.current.weather.ic}.png`" alt="" class="icon">
    <!-- <p> {{cityData.current.weather.ic }}  </p> -->
  </div>
</template>

<script>
export default {
  name: 'city-details',
  props: ['cityData'],
}
</script>

<style lang="css" scoped>
</style>
