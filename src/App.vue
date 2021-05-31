<template>
  <div id="app">
    <Maps ref="maps" />
  </div>
</template>

<script>
import Maps from './components/Maps.vue'
// import L from 'leaflet'

export default {
  name: 'App',
  components: {
    Maps
  },
  data() {
    return {
      halo: 'hola'
    }
  },
  methods: {
    addMarker() {
      // var realMap = this.$refs['maps'].map;
      // L.marker([0,115]).addTo(realMap)
    }
  }
}
</script>
