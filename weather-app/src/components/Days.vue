<template>
  <div class="card m-3" style="width: 18rem;">
    <div class="card-body">
      <div class="d-flex justify-content-between">
        <div>
          <h5 class="card-title">{{ daysData.title }}, {{ daysData.date }}</h5>
          <h6 class="card-subtitle mb-2 text-muted">{{ daysData.weather }}</h6>
        </div>
        <div>
          <component :is="icon"></component>
        </div>
      </div>
      <div class="card-text d-flex justify-content-between">
        <span>{{daysData.desc}}</span>
          <span>{{daysData.deg}}</span>
      </div>
    </div>
  </div>
</template>

<script>
const weather_map = {
  Clear: Clear,
  Snow: Snow,
  Rain: Rain,
  Clouds: Rain,
};

import Rain from "@/components/Icons/Rain.vue";
import Snow from "@/components/Icons/Snow.vue";
import Sun from "@/components/Icons/Sun.vue";
import Clear from "@/components/Icons/Clear.vue";

export default {
  props: {
    daysData: {
      type: Array,
      required: true,
    },
  },
  components: {
    Rain,
    Snow,
    Sun,
    Clear,
  },
  data() {
    return {};
  },
  computed: {
    icon() {
      return weather_map[this.daysData?.weather];
    },
  },
};
</script>
<style scoped>
.card{
  transition: 0.5s ease-in-out !important;
}
.card:hover{
  border: 1px solid grey !important;
  transform: translateY(-5px);
  cursor: pointer;
}
</style>