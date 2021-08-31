<template>
  <section>
    <div id="timeline">
      <div class="pointer"></div>
      <div class="pointer"></div>
      <div class="pointer"></div>
    </div>
    <div id="map"></div>
  </section>
</template>

<script>
export default {
  mounted() {
    this.createMap();
  },

  methods: {
    createMap() {
      const map = L.map('map').setView([49.762085, 4.726096], 13)
      L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {
        attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
        maxZoom: 18,
        id: 'mapbox/streets-v11',
        tileSize: 512,
        zoomOffset: -1,
        accessToken: 'pk.eyJ1IjoiZGR0LWFyZGVubmVzIiwiYSI6ImNrc3Qxb29xeDA5ZXkyb3BjOHI1bWZuMXYifQ.rpxnQ4xjiaFRnIFM18eP7A'
      }).addTo(map);
      const marker = L.marker([49.762085, 4.726096]).addTo(map);
    }
  }
}
</script>