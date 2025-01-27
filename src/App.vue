<template>
  <v-app>
    <v-container>
      <v-card class="mx-auto my-12" max-width="600">
        <v-card-title class="text-h5 text-center">Weather App</v-card-title>
        <v-card-subtitle class="text-center">
          Get real-time weather updates for any city
        </v-card-subtitle>

        <!-- Search Section -->
        <v-card-text>
          <WeatherSearch @searchCity="fetchWeather" />
        </v-card-text>

        <!-- Weather Display Section -->
        <v-divider></v-divider>
        <v-card-text>
          <!-- Show weather data or a message to search -->
          <WeatherDisplay v-if="weatherData" :weather="weatherData" />
          <v-alert
            v-else
            type="info"
            class="mt-4"
            dense
          >
            Enter a city to see the weather details.
          </v-alert>
        </v-card-text>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
import WeatherSearch from "./components/WeatherSearch.vue";
import WeatherDisplay from "./components/WeatherDisplay.vue";
import axios from "axios";

export default {
  components: {
    WeatherSearch,
    WeatherDisplay,
  },
  data() {
    return {
      weatherData: null, // Holds weather data
    };
  },
  methods: {
    async fetchWeather(location) {
      const apiKey = "PECSYKSZTBQ4N2H4AKG98LFZ4";
      const url = `https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${encodeURIComponent(
        location
      )}?unitGroup=metric&key=${apiKey}&contentType=json`;

      try {
        const response = await axios.get(url);
        this.weatherData = response.data;
      } catch (error) {
        console.error("Error:", error.response ? error.response.data : error.message);
        alert("City not found or API error!");
      }
    },
  },
};
</script>

<style scoped>
body {
  background-color: #f5f5f5;
  font-family: 'Roboto', sans-serif;
}

.v-card {
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

.v-btn {
  width: 100%;
}

.v-list-item-title {
  font-weight: bold;
}

.v-list-item-subtitle {
  color: #555;
}

</style>
