<template>
  <div>
    <div class="box">
      <div class="section" v-if="userIpAddress">
        <p>IP Address</p>
        <h1>
          {{ userIpAddress }}
        </h1>
      </div>
      <div class="section" v-if="country">
        <p>Location</p>
        <h1>
          {{ country }}
          {{ region }}
        </h1>
      </div>
      <div class="section" v-if="timezone">
        <p>timezone</p>
        <h1>{{ timezone }}</h1>
      </div>
      <div class="section" v-if="isp">
        <p>isp</p>
        <h1>
          {{ isp }}
        </h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ipaddressdetails",
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
