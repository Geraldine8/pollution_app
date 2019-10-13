<template lang="html">
  <div class="wrapper" v-if='cityData'>
      <div class="weather-description">
        <p>Temperature: {{cityData.current.weather.tp }} °C </p>
        <p>Humidity: {{cityData.current.weather.hu}} % </p>
        <p>Pressure: {{cityData.current.weather.pr}} hPa</p>
        <p>Wind Speed: {{cityData.current.weather.ws}} m/s</p>
      </div>
      <div class="weather-icon">
        <img :src="`images/${cityData.current.weather.ic}.png`" alt="" class="icon">
      </div>
      <div :class="`status status-${pollutionStatus.key}`">
        <img :src="`images/${pollutionStatus.key}.svg`" alt="">
        <div class="description">
          {{pollutionStatus.description}}
          <p>Pollution: {{cityData.current.pollution.aqius }} AQI - µg/m³</p>
        </div>
      </div>
    <city-map :coordinates='cityData.location.coordinates' :key='componentKey'></city-map>
  </div>
</template>

<script>
import CityMap from './CityMap.vue';

export default {
  name: 'city-details',
  props: ['cityData'],
  data(){
    return {
      pollutionStatus: '',
      componentKey: 0,
    };
  },

  beforeUpdate: function() {
    this.componentKey += 1;
    if (this.$props.cityData.current) {
      this.pollutionStatus = this.getAqs(this.$props.cityData.current.pollution.aqius);
    }
  },

  methods: {
    getAqs(airLevel) {
      switch (true) {
        case airLevel <= 50:
          return {'key':'good', 'description': 'Air Pollution Level: Good'}
          break;
        case airLevel <= 100:
          return {'key':'moderate', 'description': 'Air Pollution Level: Moderate'};
          break;
        case airLevel <= 150:
          return {'key':'unhealthy1', 'description': 'Air Pollution Level: Unhealthy for Sensitive Groups'};
          break;
        case airLevel <= 200:
          return {'key':'unhealthy2', 'description': 'Air Pollution Level: Unhealthy'};
          break;
        case airLevel <= 300:
          return {'key':'unhealthy3', 'description': 'Air Pollution Level: Very Unhealthy'};
          break;
        case airLevel <= 400:
          return {'key':'hazardous', 'description': 'Air Pollution Level: Hazardous'};
      }
    }
  },
  components: {
    "city-map" : CityMap
  }
}
</script>

<style lang="css" scoped>

.status {
  padding-top: 20px;
  width: 200px;
  height: 180px;
  text-align: center;
}

.status img {
  width: 100px;
  align-items: center;
}

.status-good {
  background-color: #a8e05f;
}

.status-moderate {
  background-color:  #fdd74b;
}

.status-unhealthy1 {
  background-color:  #fe9b57;
}
.status-unhealthy2 {
  background-color:  #fe6a69;
}
.status-unhealthy3 {
  background-color:  #a97abc;
}
.status-unhealthy4 {
  background-color:  #a87383;
}

.description{
  text-align: center;
  font-weight:bold;
}
.description p{
  margin-top: 5px;
}

.wrapper{
  margin-left: auto;
  margin-top: 20px;
  margin: 0 auto;
  width: 600px;
  display: flex;
  flex-wrap: wrap;
}
.weather-description{
  background-color: #9FE7F5;
  width: 200px;
  height: 200px;
}
.weather-description p{
  margin-left: 20px;
}
.weather-icon{
  text-align: center;
  background-color: #FAFAFB;
  width: 200px;
  height: 200px;
}
.icon {
  margin-top: 30%;
  width: 80px;
  height: 80px;
  font-weight:bold;
}

</style>


<!-- beforeUpdate: Called when data changes, before the DOM is patched.
This is a good place to access the
existing DOM before an update, e.g. to remove manually added event listeners. -->

 <!-- beforeUpdate hook runs after data changes on your component and the update cycle begins,
 right before the DOM is patched and re-rendered. It allows you to get the new state of
 any reactive data on your component before it actually gets rendered -->
