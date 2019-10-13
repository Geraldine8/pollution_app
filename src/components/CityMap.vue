<template lang="html">
  <div id="map"></div>
</template>

<script>

export default {
  name: 'city-map',
  props: ['coordinates'],
  mounted(){
    const coordinates = this.coordinates;
    const latLng = {
      lat: coordinates[1],
      lng: coordinates[0]
    };
    const map = new google.maps.Map(document.getElementById('map'), {
      zoom: 12,
      center: latLng
    });
    const marker = new google.maps.Marker({
        position: latLng,
        map: map
    });
  }
}
</script>

<style lang="css" scoped>
#map {
  height: 300px;  /* The height is 400 pixels */
  width: 600px;  /* The width is the width of the web page */
  overflow:visible;
}
</style>
