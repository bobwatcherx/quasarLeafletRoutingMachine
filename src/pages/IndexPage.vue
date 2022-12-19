<template>
  <q-page>
    <div id="youmap" style="height:500px"></div>
  </q-page>
</template>

<script setup>
  import {onMounted} from 'vue'
  import 'leaflet/dist/leaflet.css'
  import L from 'leaflet'
  import "leaflet-routing-machine/dist/leaflet-routing-machine.css";
import { IRouter, IGeocoder, LineOptions } from "leaflet-routing-machine";
import './control.geocoder.js'

window.lrmConfig = {

}

  function initmap(){

    // CREATE MAPS
    var map = L.map("youmap",{
      center:[51.505,-0.09],
      zoom:13
    })

L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png").addTo(map)

var control = L.Routing.control(L.extend(window.lrmConfig,{
  waypoints:[
    L.latLng(57.74,11.94),// START YOU MARKER LOCATION
    L.latLng(57.6792,11.945), // END YOU MARKER LOCATION
    ],
    geocoder: L.Control.Geocoder.nominatim(),
  routeWhileDragging: true,
  reverseWaypoints: true,
  showAlternatives: true,
  altLineOptions: {
    styles: [
      {color: 'black', opacity: 0.15, weight: 9},
      {color: 'white', opacity: 0.8, weight: 6},
      {color: 'blue', opacity: 0.5, weight: 2}
    ]
  }
})).addTo(map)
L.Routing.errorControl(control).addTo(map);
  }

onMounted(()=>{
  initmap()
})
</script>