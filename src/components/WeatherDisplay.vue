<template>
  <v-card class="pa-3 mb-4" outlined>
    <v-card-title class="text-h6 text-center">
      Current Weather in {{ weather.resolvedAddress }}
    </v-card-title>

    <v-card-text>
      <v-row>
        <v-col>
          <strong>Date:</strong>
          <div>{{ weather.currentConditions.datetime }}</div>
        </v-col>
        <v-col>
          <strong>Temperature:</strong>
          <div>{{ weather.currentConditions.temp }} {{ unit }}</div>
        </v-col>
      </v-row>

      <v-row>
        <v-col>
          <strong>Condition:</strong>
          <div>{{ weather.currentConditions.conditions }}</div>
        </v-col>
        <v-col>
          <strong>Humidity:</strong>
          <div>{{ weather.currentConditions.humidity }}%</div>
        </v-col>
      </v-row>

      <v-row>
        <v-col>
          <strong>Wind Speed:</strong>
          <div>{{ weather.currentConditions.windspeed }} km/h</div>
        </v-col>
        <v-col>
          <strong>Feels Like:</strong>
          <div>{{ weather.currentConditions.feelslike }} °C</div>
        </v-col>
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: "WeatherDisplay",
  props: {
    weather: Object,
    unit: {
      type: String,
      default: "°C",
    },
  },
};
</script>
