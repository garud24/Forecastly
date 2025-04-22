<template>
  <v-app :class="weatherBackgroundClass">
    <v-container>
      <v-card class="mx-auto my-12" max-width="600">
        <v-card-title class="text-h5 text-center">Forecastly</v-card-title>
        <v-card-subtitle class="text-center">
          Get real-time weather updates for any city
        </v-card-subtitle>
        <v-card-text>
          <v-switch
            v-model="useMetric"
            inset
            dense
            :label="`Units: ${useMetric ? 'Celsius (°C)' : 'Fahrenheit (°F)'}`"
            color="primary"
          ></v-switch>
        </v-card-text>

        <!-- Weather Search -->
        <v-card-text>
          <WeatherSearch @searchCity="fetchWeather" />
        </v-card-text>

        <v-card-text>
          <v-btn color="secondary" @click="useMyLocation">
            📍 Use My Location
          </v-btn>
        </v-card-text>

        <WeatherDisplay
          v-if="weatherData && weatherData.currentConditions"
          :weather="weatherData"
          :unit="useMetric ? '°C' : '°F'"
        />

        <!-- Forecast or Message -->
        <v-card-text>
          <SevenDayForecast
            v-if="weatherData"
            :forecast="weatherData.days.slice(0, 7)"
          />
          <v-alert v-else type="info" dense class="mt-4">
            Enter a city to see the forecast.
          </v-alert>
        </v-card-text>
        <TemperatureChart
          v-if="weatherData"
          :forecast="weatherData.days.slice(0, 7)"
        />
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
import axios from "axios";
import WeatherSearch from "./components/WeatherSearch.vue";
import SevenDayForecast from "./components/SevenDayForecast.vue";
import WeatherDisplay from "./components/WeatherDisplay.vue";
import TemperatureChart from "./components/TemperatureChart.vue";

export default {
  name: "App",
  components: {
    WeatherSearch,
    SevenDayForecast,
    WeatherDisplay,
    TemperatureChart,
  },
  data() {
    return {
      weatherData: null,
      useMetric: true,
    };
  },
  methods: {
    async fetchWeather(city) {
      const apiKey = "PECSYKSZTBQ4N2H4AKG98LFZ4";
      const unitGroup = this.useMetric ? "metric" : "us";
      const url = `https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${encodeURIComponent(
        city
      )}?unitGroup=${unitGroup}&key=${apiKey}&contentType=json`;

      try {
        const response = await axios.get(url);
        this.weatherData = response.data;
        console.log("Weather fetched:", this.weatherData);
      } catch (error) {
        console.error("Weather fetch error:", error);
        alert("City not found or API error!");
      }
    },

    useMyLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          (position) => {
            const coords = `${position.coords.latitude},${position.coords.longitude}`;
            this.fetchWeather(coords);
          },
          (error) => {
            console.error("Geolocation error:", error);
            alert("Unable to access location.");
          }
        );
      } else {
        alert("Geolocation is not supported by your browser.");
      }
    },
  },
  watch: {
    useMetric() {
      if (this.weatherData) {
        this.fetchWeather(this.weatherData.resolvedAddress);
      }
    },
  },
  computed: {
    weatherBackgroundClass() {
      if (!this.weatherData || !this.weatherData.currentConditions)
        return "bg-default";

      const condition =
        this.weatherData.currentConditions.conditions.toLowerCase();

      if (condition.includes("clear")) return "bg-sunny";
      if (condition.includes("cloudy")) return "bg-cloudy";
      if (condition.includes("rain") || condition.includes("drizzle"))
        return "bg-rainy";
      if (condition.includes("snow")) return "bg-snowy";
      if (condition.includes("thunder")) return "bg-thunderstorm";
      if (condition.includes("fog")) return "bg-foggy";

      return "bg-default";
    },
  },
};
</script>

<style scoped>
.v-card {
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}
.bg-default {
  background: linear-gradient(to bottom, #e0e0e0, #f5f5f5);
}

.bg-sunny {
  background: linear-gradient(to bottom, #fdd835, #ffeb3b);
}

.bg-cloudy {
  background: linear-gradient(to bottom, #90a4ae, #cfd8dc);
}

.bg-rainy {
  background: linear-gradient(to bottom, #4fc3f7, #0288d1);
}

.bg-snowy {
  background: linear-gradient(to bottom, #e1f5fe, #81d4fa);
}

.bg-thunderstorm {
  background: linear-gradient(to bottom, #616161, #9e9e9e);
}

.bg-foggy {
  background: linear-gradient(to bottom, #cfd8dc, #eceff1);
}

</style>
