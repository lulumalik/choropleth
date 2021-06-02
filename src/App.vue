<template>
  <div style="position:relative">
    <Search style="position:absolute;right:5px;top:5px;z-index:1000" @searching="searchLocation"/>
    <Maps ref="maps" />
  </div>
</template>

<script>
import Search from './components/Search'
import Maps from './components/Maps.vue'
import L from 'leaflet'

export default {
  name: 'App',
  components: {
    Search,
    Maps
  },
  data() {
    return {
      halo: 'hola'
    }
  },
  methods: {
    searchLocation(obj) {
      var maps = this.$refs['maps'].map
      // clear marker sebelum add
      L.marker(obj.geometry.coordinates.reverse()).addTo(maps)
      maps.setView(obj.geometry.coordinates, 8)
    },
    addMarker() {
      // var realMap = this.$refs['maps'].map;
      // L.marker([0,115]).addTo(realMap)
    }
  }
}
</script>
