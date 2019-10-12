<template lang="html">
  <div v-if='cityData'>
    <div class="wrapper">
      <div>
        <p>Temperature: {{cityData.current.weather.tp }} °C </p>
        <p>Humidity: {{cityData.current.weather.hu}} % </p>
        <p>Pressure: {{cityData.current.weather.pr}} hPa</p>
        <p>Wind Speed: {{cityData.current.weather.ws}} m/s</p>
      </div>
      <img :src="`images/${cityData.current.weather.ic}.png`" alt="" class="icon">
    </div>
    <div :class="`status status-${pollutionStatus.key}`">
      <img :src="`images/${pollutionStatus.key}.svg`" alt="">
      <div class="description">
        {{pollutionStatus.description}}
        <p>Pollution: {{cityData.current.pollution.aqius }} AQI - µg/m³</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'city-details',
  props: ['cityData'],
  data(){
    return {
      pollutionStatus: 'culo'
    };
  },
  beforeUpdate: function() {
    if (this.$props.cityData.current) {
      this.pollutionStatus = this.getAqs(this.$props.cityData.current.pollution.aqius);
    }
  },
  methods: {
    getAqs(airLevel) {
      switch (true) {
        case airLevel <= 50:
          return {'key':'good', 'description': 'Air Pollution Lelvel: Good'}
          break;
        case airLevel <= 100:
          return {'key':'moderate', 'description': 'Air Pollution Lelvel: Moderate'};
          break;
        case airLevel <= 150:
          return {'key':'unhealthy1', 'description': 'Air Pollution Lelvel: Unhealthy for Sensitive Groups'};
          break;
        case airLevel <= 200:
          return {'key':'unhealthy2', 'description': 'Air Pollution Lelvel: Unhealthy'};
          break;
        case airLevel <= 300:
          return {'key':'unhealthy3', 'description': 'Air Pollution Lelvel: Very Unhealthy'};
          break;
        case airLevel <= 400:
          return {'key':'hazardous', 'description': 'Air Pollution Lelvel: Hazardous'};
      }
    }
  }
}
</script>

<style lang="css" scoped>

.status{
  width: 300px;
  padding-top: 40px;
  padding-bottom: 40px;
  text-align: center;
}

.status img {
  width: 150px;
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
  display: flex;
  flex-wrap: wrap;
}

.icon {
  width: 150px;
  vertical-align:top;
  display:inline-block;
  font-weight:bold;
}
</style>
