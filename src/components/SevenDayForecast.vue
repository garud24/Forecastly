<template>
  <v-slide-group v-if="forecast && forecast.length" show-arrows class="mt-4">
    <v-slide-item v-for="(day, index) in forecast" :key="index">
      <v-card class="mx-2 pa-3" width="130" outlined>
        <div class="text-center font-weight-medium">
          {{ formatDate(day.datetime) }}
        </div>
        <div class="text-center">🌡️ {{ day.temp }}°</div>
        <div class="text-center">
          {{ conditionIcons[day.conditions] || "🌈" }} {{ day.temp }}°
        </div>
      </v-card>
    </v-slide-item>
  </v-slide-group>
</template>

<script>
import { DateTime } from "luxon";

export default {
  name: "SevenDayForecast",
  props: {
    forecast: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      conditionIcons: {
        Clear: "☀️",
        "Partially cloudy": "⛅",
        Cloudy: "☁️",
        Rain: "🌧️",
        Snow: "❄️",
        Thunderstorm: "🌩️",
        Fog: "🌫️",
        Overcast: "☁️",
        Drizzle: "🌦️",
      },
    };
  },
  methods: {
    formatDate(dateStr) {
      return DateTime.fromISO(dateStr).toFormat("ccc, dd LLL");
    },
    getIcon(condition) {
      const conditionIcons = {
        Clear: "☀️",
        "Partially cloudy": "⛅",
        Cloudy: "☁️",
        Rain: "🌧️",
        Snow: "❄️",
        Thunderstorm: "🌩️",
        Fog: "🌫️",
        Overcast: "☁️",
        Drizzle: "🌦️",
      };
      return conditionIcons[condition] || "🌈";
    },
  },
};
</script>

<style scoped>
.v-card {
  text-align: center;
  font-size: 14px;
}
</style>
