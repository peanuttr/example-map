<template>
  <div id="map">
    <div class="box">
      <input type="text" v-model="keyword" />
      <button @click="onSearch">Search</button>
    </div>
    <div id="map">
      <LongdoMap @load="event" >
        <LongdoMapMarker v-for="(item, i) in markers"             
            :key="i"             
            :location="item.location"
            :title="item.title"             
            :detail="item.detail" />
      </LongdoMap>
    </div>
  </div>
</template>

<script>
import { LongdoMap, LongdoMapMarker } from "longdo-map-vue";
import axios from "axios";
LongdoMap.init({
  apiKey: "8a5564754580b3cda676ad2ebf437179",
  placeholder: document.getElementById("map"),
});

export default {
  name: "MyComponent",
  components: {
    LongdoMap,
    LongdoMapMarker,
  },
  data() {
    return {
      keyword: "",
      markers: [
        {
          location: {
            lon: Number,
            lat: Number,
          },
          title: "",
          detail: "",
        },
      ],
    };
  },
  methods: {
    onSearch() {
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.keyword}&appid=76a5fd9779d2cd32c52aef182e657372`
        )
        .then((data) => {
          this.markers.push({location:{
            lon:data.data.coord.lon,
            lat:data.data.coord.lat,
          }})
          console.log(this.markers);
          // map.location({ lon: data.data.coord.lon, lat: data.data.coord.lat });
        });
    },
    event(map) {
      map.Ui.Crosshair.visible(false);
    },
  },
};
</script>

<style>
#map {
  height: 100vh;
}
.box{
  display: flex;
  justify-content: center;
}
</style>