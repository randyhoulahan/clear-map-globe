<template>
  <div id="mapView">

  </div>
</template>

<script>
import                "@arcgis/core/assets/esri/themes/dark/main.css"
import SceneView from "@arcgis/core/views/SceneView"
import Map from       "@arcgis/core/Map"
import config from    "@arcgis/core/config"
import TileLayer from "@arcgis/core/layers/TileLayer"
import Basemap from   '@arcgis/core/Basemap'



const key = "AAPK646a81c542644891abe68e9b21413e7d9MDczfDifZi8IyvG6QcxfFuNqSRmlqH95-PH9mBOSEf4a4eE2Nwt8wIRsBLWd4NO"

export default {
  name: 'ArcGisMapBase',
  data, mounted
}

function data(){
  return { map: undefined }
}
function mounted(){
  config.apiKey = key



  const basemap = new Basemap({
    baseLayers: [ new TileLayer({ url: "https://geoservices.un.org/arcgis/rest/services/ClearMap_Dark/MapServer", }), ],//
    //baseLayers: [ new TileLayer({ url: "https://tiles.arcgis.com/tiles/nGt4QxSblgDfeJn9/arcgis/rest/services/terrain_with_heavy_bathymetry/MapServer", }), ],
  })        
  

  const map = new Map({ basemap })



    const view = new SceneView({
          container: "mapView",
          map: map,
          alphaCompositingEnabled: true,
          qualityProfile: "high",
          viewingMode: "global",
          camera: {
            position: [-55.03975781, 14.94826384, 19921223.30821],
            heading: 2.03,
            tilt: 0.13,
          },
          environment: {
            background: { type: "color", color: [255, 252, 244, 0], },
            starsEnabled: false,
            atmosphereEnabled: false,
            lighting: {
              directShadowsEnabled: false,
              date:
                "Sun Jun 23 2019 19:19:18 GMT+0200 (Central European Summer Time)",
            },
          },
          constraints: {
            altitude: { min: 10000000, max: 25000000, },
          },
          popup: {
            dockEnabled: true,
            dockOptions: { position: "top-right", breakpoint: false, buttonEnabled: false, },
            collapseEnabled: false,
          },
          highlightOptions: { color: [255, 255, 255], haloOpacity: 0.5, },
        })

        console.log('view', view)
}
</script>
<style scoped>
 #mapView {
        padding: 0;
        margin: 0;
        height: 60vh;
        width: 100%;
        background: radial-gradient(#91c7e3, #3d93bf);
      }
</style>