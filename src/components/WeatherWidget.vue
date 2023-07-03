<template>
    <div class="custom-weather-widget">
      <h2 class="custom-widget-title">Custom Weather Widget</h2>
      <div class="custom-location-input">
        <label for="custom-location">Enter Custom Location:</label>
        <input type="text" id="custom-location" v-model="customLocation" />
        <button @click="fetchCustomWeatherData">Get Custom Weather</button>
      </div>
      <div v-if="customWeatherData" class="custom-weather-data">
        <p class="custom-location">Custom Location: {{ customWeatherData.name }}</p>
        <p v-if="customWeatherData.main" class="custom-temperature">
          Custom Temperature: {{ customWeatherData.main.temp }}°C
        </p>
        <p v-if="customWeatherData.weather" class="custom-description">
          Custom Description: {{ customWeatherData.weather[0].description }}
        </p>
      </div>
      <p v-else>Loading custom weather data...</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        customLocation: '',
        customWeatherData: null
      };
    },
    methods: {
      async fetchCustomWeatherData() {
        try {
          const apiKey = 'YOUR_API_KEY';
          const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.customLocation}&appid=${apiKey}`;
          const response = await fetch(apiUrl);
          const data = await response.json();
          this.customWeatherData = data;
        } catch (error) {
          console.error('Error fetching custom weather data:', error);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .custom-weather-widget {
    border: 1px solid #df8d8d;
    padding: 20px;
    margin-bottom: 20px;
    text-align: center;
    background-color: #5ca06d;
  }
  
  .custom-widget-title {
    margin-top: 0;
    color: #8657bb;
  }
  
  .custom-location-input {
    margin-bottom: 10px;
  }
  
  .custom-weather-data {
    margin-top: 10px;
  }
  
  .custom-location {
    font-size: 18px;
    font-weight: bold;
  }
  
  .custom-temperature {
    font-size: 24px;
    color: #fa3f06;
  }
  
  .custom-description {
    font-size: 16px;
  }
  </style>
  