<template>
    <div ref="geoLocationControl" class="leaflet-control leaflet-bar">
        <button @click="locateUser" title="Localizar">
            <i class="fa fa-location-arrow"></i>
        </button>
    </div>
</template>
  
<script>
import L from 'leaflet';

export default {
    name: 'GeoLocation',
    props: {
        map: Object
    },
    mounted() {
        this.$nextTick(() => {
            this.addControlToMap();
        });
    },
    unmounted() {
        this.map.off('locationfound');
        this.map.off('locationerror');
    },
    methods: {
        addControlToMap() {
            if (this.map) {
                const controlElement = this.$refs.geoLocationControl;
                const Control = L.Control.extend({
                    onAdd: () => {
                        return controlElement;
                    }
                });
                new Control({ position: 'topleft' }).addTo(this.map);
            }
        },
        locateUser() {
            if ('geolocation' in navigator) {
                navigator.geolocation.getCurrentPosition(
                    position => {
                        this.setMapLocation(position.coords.latitude, position.coords.longitude);
                    },
                    error => {
                        console.log('Navigator geolocation is not available.', error);

                        this.locateWithLeaflet();
                    }
                );
            }
            else {
                console.log('Navigator geolocation is not available.');

                this.locateWithLeaflet();
            }
        },
        locateWithLeaflet() {
            this.map.locate({
                setView: true,
                maxZoom: 16,
                enableHighAccuracy: true
            });

            this.map.on('locationfound', e => {
                this.setMapLocation(e.latitude, e.longitude);
            });

            this.map.on('locationerror', e => {
                console.error('Leaflet Geolocation error:', e);
            });
        },
        setMapLocation(lat, lng) {
            if (this.map) {
                this.map.setView([lat, lng], 13);
                L.marker([lat, lng]).addTo(this.map);
            }
        }
    }
};
</script>

<style>

</style>