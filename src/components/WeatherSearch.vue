<template>
  <v-row>
    <v-col>
      <v-text-field
        v-model="searchInput"
        label="Enter city name"
        outlined
        dense
        clearable
      ></v-text-field>
    </v-col>
    <v-col cols="auto">
      <v-btn color="primary" @click="onSearch" :disabled="!searchInput">
        Search
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'WeatherSearch',
  data() {
    return {
      searchInput: '',
    };
  },
  methods: {
    onSearch() {
      this.$emit('searchCity', this.searchInput);
    },
  },
};
</script>
