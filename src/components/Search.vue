<template>
  <div>
    <input
      type="text"
      style="padding: 3px"
      v-model="searching"
      @keyup="searchDataMethod($event)"
      placeholder="Location ..."
    />

    <div v-if="list.length > 0">
      <div
        v-for="(value, index) in list"
        :key="index"
        @click="searchData(value)"
        style="
          cursor: pointer;
          padding: 5px;
          border: 1px solid #000;
          margin-top: 5px;
        "
      >
        <div>{{ value.properties.name }}</div>
        <div>{{ value.properties.region }}</div>
        <div>{{ value.properties.locality }}</div>
        <div>{{ value.properties.country }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      searching: "",
      list: [],
    };
  },
  methods: {
    searchData(obj) {
      this.$emit("searching", obj);
    },
    searchDataMethod(e) {
      //   console.log(e.target.value);
      var val = e.target.value;
      if (val !== "" && val.length > 3) {
        axios
          .get(
            `https://api.openrouteservice.org/geocode/search?api_key=5b3ce3597851110001cf6248b92552d10a984cd0b0203a875a9341a2&text=${val}`
          )
          .then((res) => {
            this.list = res.data.features;
          });
      }
    },
  },
  watch: {
    searching() {
      //   setTimeout(() => {
      // bandun , g gk dapet
      // if (val !== "" && val.length > 3) {
      //   axios
      //     .get(
      //       `https://api.openrouteservice.org/geocode/search?api_key=5b3ce3597851110001cf6248b92552d10a984cd0b0203a875a9341a2&text=${val}`
      //     )
      //     .then((res) => {
      //       this.list = res.data.features
      //     });
      // }
      //   }, 1000);
    },
  },
};
</script>