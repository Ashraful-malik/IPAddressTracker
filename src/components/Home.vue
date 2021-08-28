<template>
  <div>
    <IpAddressDetails
      v-bind:userIpAddress="userIpAddress"
      v-bind:isp="isp"
      v-bind:timezone="timezone"
      v-bind:country="country"
      v-bind:region="region"
      v-bind:lat="lat"
      v-bind:lng="lng"
    />
    <div class="search">
      <h2>iP Address Tracker</h2>
      <div class="search_box">
        <input
          type="text"
          placeholder="Search for any IP address or domain"
          class="text_field"
          v-model="ipaddress"
          @keyup.enter="fetchApiData"
        />
        <button v-on:click="fetchApiData">
          <img src="@/assets/images/icon-arrow.svg" alt="" />
        </button>
      </div>
    </div>
    <div class="map_container">
      <div id="mymap"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import locationImage from "../assets/images/icon-location.svg";
import IpAddressDetails from "./IpAddressDetails.vue";
import L from "leaflet";
export default {
  name: "home",
  components: {
    IpAddressDetails,
  },
  data() {
    return {
      ipaddress: "",
      userIpAddress: "",
      isp: "",
      timezone: "",
      region: "",
      country: "",
      lat: "",
      lng: "",
    };
  },
  methods: {
    fetchApiData(e) {
      const url = `https://geo.ipify.org/api/v1?apiKey=at_AF6Ygh72glF3cehljUp6B7j2zMbpp&ipAddress=${this.ipaddress}`;
      axios
        .get(url)
        .then((res) => {
          this.isp = res.data.isp;
          this.userIpAddress = res.data.ip;
          this.timezone = res.data.location.timezone;
          this.region = res.data.location.region;
          this.country = res.data.location.country;
          this.lat = res.data.location.lat;
          this.lng = res.data.location.lng;
          // console.log(this.lng);
          const mymap = L.map("mymap").setView([this.lat, this.lng], 9);
          var myIcon = L.icon({
            iconUrl: locationImage,
          });
          L.marker([this.lat, this.lng], { icon: myIcon }).addTo(mymap);

          L.tileLayer(
            `https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=${process.env.VUE_APP_MAP_BOX_API_KEY}`,
            {
              attribution:
                'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
              maxZoom: 18,
              id: "mapbox/streets-v11",
              tileSize: 512,
              zoomOffset: -1,
              accessToken: process.env.VUE_APP_MAP_BOX_API_KEY,
            }
          ).addTo(mymap);
        })
        .catch((err) => {
          console.log(err);
        });
      e.target.value = "";
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/sass/main.scss";
</style>
