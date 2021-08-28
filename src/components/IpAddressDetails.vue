<template>
  <div>
    <div class="box">
      <div class="section">
        <p>IP Address</p>
        <Loader v-if="!userIpAddress" />
        <h1>
          {{ userIpAddress }}
        </h1>
      </div>
      <div class="section">
        <p>Location</p>
        <Loader v-if="!userIpAddress" />
        <h1>
          {{ country }}
          {{ region }}
        </h1>
      </div>
      <div class="section">
        <p>timezone</p>
        <Loader v-if="!userIpAddress" />
        <h1>
          {{ timezone }}
        </h1>
      </div>
      <div class="section">
        <p>isp</p>
        <Loader v-if="!isp" />
        <h1>
          {{ isp }}
        </h1>
      </div>
    </div>
  </div>
</template>

<script>
import Loader from "./Loader.vue";
export default {
  name: "ipaddressdetails",
  components: {
    Loader,
  },
  props: [
    "userIpAddress",
    "isp",
    "timezone",
    "country",
    "lat",
    "lng",
    "region",
  ],
};
</script>

<style lang="scss" scoped>
@import "@/assets/sass/main.scss";
</style>
