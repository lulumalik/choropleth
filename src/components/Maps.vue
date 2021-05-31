<template>
  <div class="hello">
    <div style="position: relative">
      <div style="position: absolute; right: 0; top: 0; z-index: 1000000">
        Data Click Geojson
        <div>
          <table>
            <tbody>
              <tr v-for="(value, key) in dataClick" :key="key">
                <td>{{ key }}</td>
                <td>{{ value }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <div id="map" style="height: 90vh; widht: 100vw"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import L from "leaflet";
export default {
  data() {
    return {
      map: null,
      dataClick: {},
    };
  },
  mounted() {
    this.map = L.map("map", {
      center: [40.745255, -74.034775],
      zoom: 5,
    });

    L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png").addTo(
      this.map
    );

    axios.get("/us.json").then((res) => {
      // console.log(res)
      L.geoJson(res.data, {
        style: this.styling, // this + . + nama function
        onEachFeature: this.onEachFeature,
      }).addTo(this.map);
    });
  },
  methods: {
    styling(e) {
      return {
        fillColor: this.getColor(e.properties.density), // javascript khususnya di vue , akses methods selalu this.
        weight: 1,
        opacity: 1,
        color: "white",
        dashArray: "3",
        fillOpacity: 0.7,
      };
    },
    onEachFeature(feature, layer) {
      var that = this;
      layer.on("click", function (e) {
        that.dataClick = e.target.feature.properties;
      });
      // console.log(e, "eachfeature");
    },
    getColor(d) {
      return d > 1000
        ? "#800026"
        : d > 500
        ? "#BD0026"
        : d > 200
        ? "#E31A1C"
        : d > 100
        ? "#FC4E2A"
        : d > 50
        ? "#FD8D3C"
        : d > 20
        ? "#FEB24C"
        : d > 10
        ? "#FED976"
        : "#FFEDA0";
    },
  },
};
</script>