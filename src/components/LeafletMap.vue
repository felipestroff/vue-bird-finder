<template>
    <div id="map"></div>
    <GeoLocation :map="map" />
</template>
  
<script>
import L from 'leaflet';
import GeoLocation from './GeoLocation.vue';

import '@fortawesome/fontawesome-free/css/all.css';

export default {
    components: {
        GeoLocation
    },
    data() {
        return {
            map: null
        };
    },
    mounted() {
        this.initMap();
    },
    methods: {
        initMap() {
            this.map = L.map('map').setView([-30, -51], 3);
            L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                maxZoom: 19,
                attribution: '© OpenStreetMap contributors'
            }).addTo(this.map);
        }
    }
};
</script>

<style>
@import "~leaflet/dist/leaflet.css";

#map {
    width: 100%;
    height: 100vh;
}

.leaflet-control button {
    width: 30px;
    height: 30px;
    line-height: 30px;
}
</style>