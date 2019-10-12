<template lang="html">
  <div v-if='cityData'>
    <div class="">
      <p>Temperature: {{cityData.current.weather.tp }} °C </p>
      <p>Humidity: {{cityData.current.weather.hu}} % </p>
      <p>Pressure: {{cityData.current.weather.pr}} hPa</p>
      <p>Wind Speed: {{cityData.current.weather.ws}} m/s</p>
      <img :src="`images/${cityData.current.weather.ic}.png`" alt="" class="icon">
    </div>
    <div class="">
    <p>Pollution: {{cityData.current.pollution.aqius }} AQI - µg/m³</p>
    <span> {{getAqs(cityData.current.pollution.aqius )}} </span>
    <img :src="`images/${getAqs(cityData.current.pollution.aqius)}.svg`" alt="" class="icon">
    <!-- <span v-if='cityData.current.pollution.aqius >= 100'>
      Moderate
    </span>
    <span v-if='cityData.current.pollution.aqius >= 150'>
      Unhealthy for Sensitive Groups
    </span> -->
    </div>

  </div>
</template>

<script>
export default {
  name: 'city-details',
  props: ['cityData'],

  methods: {
    getAqs(airLevel) {
      switch (true) {
        case airLevel <= 50:
          return 'good' ;
          break;
        case airLevel <= 100:
          return 'Moderate';
          break;
        case airLevel <= 150:
          return 'Unhealthy for Sensitive Groups';
          break;
        case airLevel <= 200:
          return 'Unhealthy'
          break;
        case airLevel <= 300:
          return 'Very Unhealthy';
          break;
        case airLevel <= 400:
          return 'Hazardous'
      }
    }
  }
}
</script>

<style lang="css" scoped>
</style>
