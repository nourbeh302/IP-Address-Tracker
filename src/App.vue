<template>
  <section class="App">
    <div class="container">
      <h2>IP Address Tracker</h2>
      <div class="input-field">
        <input type="text" placeholder="Enter an IP Address or press ENTER" v-model="query" @keyup.enter="fetchIPInfo" />
        <span class="icon">
          <img src="./assets/arrow-right.svg" alt="" srcset="" />
        </span>
      </div>
      <IPCard :IPInfo="IPInfo" v-if="IPInfo" />
    </div>
    <div id="map"></div>
  </section>
</template>

<script>
import IPCard from "./components/IPCard.vue";
import { onMounted, ref } from "vue";
import L from "leaflet";
import "leaflet/dist/leaflet.css";

import marker from "./assets/marker.svg";

export default {
  name: "App",
  components: { IPCard },
  setup() {
    let myMap;
    let query = ref("");
    let IPInfo = ref(null);

    let markerIcon = L.icon({
      iconUrl: marker,
      iconSize: [23, 28],
      iconAnchor: [16, 17],
    });

    // Loading map
    onMounted(() => {
      let lng = 31.308952111,
        lat = 30.10093501241242;
      let myHomeLngLat = [lat, lng];

      myMap = L.map("map").setView(myHomeLngLat, 18);
      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png").addTo(
        myMap
      );
    });

    // Fetching IPInfo
    async function fetchIPInfo() {
      try {
        let response = await fetch(
          `https://geo.ipify.org/api/v1?apiKey=at_RBfgufKhpizoxKa5DY66rJqyW6VVx&ipAddress=${query.value}`
        );

        let result = await response.json();

        IPInfo.value = {
          address: result.ip,
          state: result.location.city,
          timezone: result.location.timezone,
          isp: result.isp,
          lat: result.location.lat,
          lng: result.location.lng,
        };

        // Updating map view & marker
        myMap.setView([IPInfo.value.lat, IPInfo.value.lng], 13);
        L.marker([IPInfo.value.lat, IPInfo.value.lng], { icon: markerIcon }).addTo(myMap);

      } catch (error) {
        console.log(error);
      }
    }

    return {
      query,
      IPInfo,
      fetchIPInfo,
    };
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

:root {
  --clr-primary: hsl(210, 100%, 31%);
  --clr-white: hsl(180, 0%, 95%);
  --clr-black: hsl(180, 0%, 10%);
  --clr-grey: hsl(180, 0%, 35%);
  --shadow: hsla(180, 0%, 10%, 50%);
  --ff-text: "DM Sans", sans-serif;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: var(--ff-text);
}

.App {
  height: 100vh;
  display: grid;
  grid-template-rows: 4fr 9fr;
}

.container {
  gap: 1em;
  background: url("./assets/pattern-bg.png") no-repeat center center;
  background-size: cover;
  padding: 2em;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

.container>h2 {
  color: var(--clr-white);
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: 400;
}

.input-field {
  display: flex;
  width: min(480px, 50%);
}

.input-field>input {
  height: 100%;
  padding-inline: 1em;
  width: 100%;

  outline: none;
  border-radius: 4px 0px 0px 4px;
  border: none;
  text-overflow: ellipsis;

  font-size: 16px;
}

.input-field>span.icon {
  border-radius: 0px 4px 4px 0px;
  padding: 14px;
  height: 44px;
  background: var(--clr-black);
}

img {
  width: auto;
  height: 100%;
  object-fit: cover;
}

#map * {
  z-index: 2;
}

.leaflet-bottom.leaflet-right {
  display: none;
}

@media all and (max-width: 767px) {
  .input-field {
    width: 100%;
  }
}
</style>
