<template>
  <div id="map"></div>
</template>

<script>
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'
import 'leaflet.chinatmsproviders'
import * as esri from 'esri-leaflet'
import icon from 'leaflet/dist/images/marker-icon.png'
import iconShadow from 'leaflet/dist/images/marker-shadow.png'
const DefaultIcon = L.icon({
  iconUrl: icon,
  shadowUrl: iconShadow
})
L.Marker.prototype.options.icon = DefaultIcon
export default {
  name: 'Map',
  data() {
    return {
      map: '',
      map_config: {
        zoom: 15,
        center: [31.867316649619237, 117.27596282958986]
      },
      optios: {
        minZoom: 1,
        maxZoom: 18,
        key: 'eb35dddb3aa33c7a8fb4218b39d1e424'
      }
    }
  },
  methods: {
    initMap() {
      this.map = L.map('map', this.map_config)
      L.tileLayer
        .chinaProvider('GaoDe.Normal.Map', this.options)
        .addTo(this.map)
      esri
        .dynamicMapLayer({
          url:
            'http://data.marsgis.cn/arcgis/rest/services/mars/hefei/MapServer',
          layers: [24, 34]
        })
        .addTo(this.map)
      this.map.on('click', e => {
        console.log(e)
      })
    }
  },
  mounted() {
    this.initMap()
  }
}
</script>

<style>
html,
body {
  margin: 0;
}
#map {
  height: 100vh;
}
</style>
