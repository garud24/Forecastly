<template>
    <v-card class="pa-3">
      <v-card-title class="text-h6 text-center">
        Weather in {{ weather.resolvedAddress }}
      </v-card-title>
  
      <v-card-text>
        <v-row>
          <v-col>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Date:</v-list-item-title>
                <v-list-item-subtitle>{{ weather.currentConditions.datetime }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-col>
          <v-col>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Temperature:</v-list-item-title>
                <v-list-item-subtitle>{{ weather.currentConditions.temp }} °C</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-col>
        </v-row>
  
        <v-row>
          <v-col>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Condition:</v-list-item-title>
                <v-list-item-subtitle>{{ weather.currentConditions.conditions }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-col>
          <v-col>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Humidity:</v-list-item-title>
                <v-list-item-subtitle>{{ weather.currentConditions.humidity }}%</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-col>
        </v-row>
  
        <v-row>
          <v-col>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Wind Speed:</v-list-item-title>
                <v-list-item-subtitle>{{ weather.currentConditions.windspeed }} km/h</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-col>
          <v-col>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Feels Like:</v-list-item-title>
                <v-list-item-subtitle>{{ weather.currentConditions.feelslike }} °C</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </template>
  
  <script>
  export default {
    props: {
      weather: Object,
    },
  };
  </script>
  