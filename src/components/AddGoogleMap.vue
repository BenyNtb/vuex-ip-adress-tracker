<template>
<client-only>
  <l-map style="height: 300px" :zoom="zoom" :center="center">
    <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    <l-marker :lat-lng="markerLatLng" ></l-marker>
  </l-map>
</client-only>  
</template>

<script>
import {LMap, LTileLayer, LMarker} from 'vue2-leaflet';

export default {
    components: {
        LMap,
        LTileLayer,
        LMarker
    },
    data () {
        return {
        url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
        attribution:
            '&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
        zoom: 15,
        center: [50.8500, 4.3500],
        markerLatLng: [50.8500, 4.3500]
        };
    },
    
}
</script>

<style scoped>
#map { height: 180px; }
</style>