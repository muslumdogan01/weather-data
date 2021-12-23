<template>
  <div id="today" class="card mt-3 mb-3" style="width: 18rem;">
    <div class="card-body">
      <div class="row d-flex mt-3">
        <div class="col-md-4">
          <component :is="icon" />
        </div>
        <div class="col-md-8 mt-2 d-flex align-items-start flex-column">
          <p class="mb-0 fs-6">Today</p>
          <span class="fs-6"> {{ showDate }} </span>
        </div>
      </div>
      <div class="row">
        <div class="d-flex align-items-start flex-column">
          <span class="fs-1 text-left mt-3">39</span>
          <span>Charlestown, RI 02813</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const weather_map = {
  Clear: Sun,
  Snow: Snow,
  Rain: Rain,
  Clouds: Rain,
};
let unix = 1640282400;
let date = new Date(unix * 1000).toDateString();


import Rain from "@/components/Icons/Rain.vue";
import Snow from "@/components/Icons/Snow.vue";
import Sun from "@/components/Icons/Sun.vue";

export default {
  name: "Today",
  components: {
    Rain,
    Snow,
    Sun,
  },
  props: {
    dailyData: {
      type: Array,
      require: true,
    },
    childDailyIcon: {
      type: Object,
      require: true,
    },
  },
  data() {
    return {
      dailyIcon: null,
      showDate: null,
      todayData: [],
    };
  },
  computed: {
    icon() {
      return weather_map[this.childDailyIcon?.weather[0].main];
    },
  },
  mounted() {
    this.showDate = date;
  },
};
</script>

<style scoped>
#today {
  background-color: rgb(183, 171, 125);
  color: white;
}
.fs-1 {
  font-size: 70px !important;
}
</style>
