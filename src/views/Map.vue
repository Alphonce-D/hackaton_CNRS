<template>
  <section>
    <div id="timeline">
      <div class="periode" id="antiquite">
        <div class="pointer" @click="antiMarker(this.gisements)"></div>
        <p>Antiquité</p>
      </div>
      <div class="periode" id="moderne">
        <div class="pointer" @click="modernMarker(this.gisements)"></div>
        <p>Epoque Moderne</p>
      </div>
      <div class="periode" id="romaine">
        <div class="pointer" @click="romainMarker(this.gisements)"></div>
        <p>Epoque Romaine</p>
      </div>
    </div>
    <div id="map"></div>
  </section>
</template>

<script>

import axios from 'axios';

export default {
  data: () => ({
    gisements: null,
    layerGroup: null,
  }),

  async mounted() {
    const response = await axios({
      method: 'GET',
      url: 'http://localhost:3000/coordinates',
    })
    this.gisements = response.data;
    this.createMap(this.gisements);
  },

  methods: {
    

    createMap(coords) {
      const map = L.map('map').setView([49.1182, 0.9582], 13)
      L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {
        attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
        maxZoom: 10,
        id: 'mapbox/streets-v11',
        tileSize: 512,
        zoomOffset: -1,
        accessToken: 'pk.eyJ1IjoiZGR0LWFyZGVubmVzIiwiYSI6ImNrc3Qxb29xeDA5ZXkyb3BjOHI1bWZuMXYifQ.rpxnQ4xjiaFRnIFM18eP7A'
        }).addTo(map);
        this.layerGroup = L.layerGroup().addTo(map);
      // coords.forEach(item => {
      //   L.marker( [item.x, item.y] ).addTo(map);
      // });
      for(let i = 0; i < 20; i++) {
        const marker = L.marker( [coords[i].x, coords[i].y] ).addTo(this.layerGroup);
        marker.on('click', this.redirect);
        marker.on('mouseover', () => {
          marker.openPopup();
        });
      }

    },


  antiMarker(coords) {
    this.layerGroup.clearLayers();
     for(let i = 0; i < 20; i++) {
      const marker = L.marker( [coords[i].x, coords[i].y]).addTo(this.layerGroup);
      marker.on('click', this.redirect);
      marker.on('mouseover', () => {
        marker.openPopup();
      });
    }
  },

  modernMarker(coords) {
    this.layerGroup.clearLayers();
    for(let i = 21; i < 47; i++) {
      const marker = L.marker( [coords[i].x, coords[i].y]).addTo(this.layerGroup);
      marker.on('click', this.redirect);
      marker.on('mouseover', () => {
        marker.openPopup();
      });
    }
},

  romainMarker(coords) {
    this.layerGroup.clearLayers();
    for( let i = 48; i < 59; i++) {
      const marker = L.marker( [coords[i].x, coords[i].y] ).addTo(this.layerGroup);
      marker.on('click', this.redirect);
      marker.on('mouseover', () => {
        marker.openPopup();
      });

    }
  },

  redirect() {
    window.location = 'https://lopez.simplon-charleville.fr/preprod/Quizz_poo_js/';
  }
    
  }
}
</script>