<template>
  <div class="container mt-5">
    <div id="wrapper" class="col d-flex w-100 justify-content-center">
      <div class="row w-25">
        <Today :dailyData="dailyData" :childDailyIcon="dailyIcon" />
      </div>

      <div class="row w-75 d-flex justify-content-center">
        <Days v-for="item in daysData" :key="item.id" :daysData="item" />
      </div>
      <div></div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Today from "@/components/Today.vue";
import Days from "@/components/Days.vue";
import db from "@/db.json";
const axios = require("axios");

export default {
  name: "Home",
  components: {
    Today,
    Days,
  },
  data() {
    return {
      dailyData: [],
      dailyIcon: null,
      daysData: db.days,
    };
  },
  mounted() {
    this.getDataList();
  },

  methods: {
    getDataList() {
      const url = "https://api.openweathermap.org/data/2.5/onecall?";
      const key = "&appid=acfb937c3577744b220977179eab6dd1";
      const params = "lat=38.42&units=metric&lon=27.14&exclude=hourly&lang=tr";
      axios
        .get(`${url}${params}${key}`)
        .then((response) => {
          // handle success
          this.dailyData = response.data.daily;
          this.dailyIcon = response.data.daily[0];
          console.log("t", this.dailyData);
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        })
        .then(function () {
          // always executed
        });
    },
  },
};
</script>

<style scoped>
@media (max-width: 576px) { 
  #wrapper{
    display: flex !important;
    flex-direction: column !important;
    justify-content: center !important;
    align-items: center !important;
  }
  #wrapper .row{
    width: 75% !important;
  }
 }
</style>