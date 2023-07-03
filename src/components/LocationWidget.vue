<template>
    <div class="custom-location-widget">
      <h2>Your Custom Location</h2>
      <div v-if="latitude && longitude">
        <p>Custom Latitude: {{ latitude }}</p>
        <p>Custom Longitude: {{ longitude }}</p>
      </div>
      <div v-else>
        <p>Finding your custom location...</p>
      </div>
  
      <div class="location-input">
        <label for="custom-latitude">Custom Latitude:</label>
        <input type="text" id="custom-latitude" v-model="inputLatitude" />
      </div>
      <div class="location-input">
        <label for="custom-longitude">Custom Longitude:</label>
        <input type="text" id="custom-longitude" v-model="inputLongitude" />
      </div>
  
      <button @click="fetchCustomLocationDetails">Find Custom Location Details</button>
  
      <div v-if="foundCustomLocation">
        <h3>Custom Location Details</h3>
        <p>{{ foundCustomLocation.components.country }}</p>
        <p>{{ foundCustomLocation.components.city }}</p>
        <p>{{ foundCustomLocation.components.street }}</p>
        <p>Custom Postal Code: {{ foundCustomLocation.components.postcode }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        latitude: null,
        longitude: null,
        inputLatitude: '',
        inputLongitude: '',
        foundCustomLocation: null,
      };
    },
    mounted() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.getCustomPosition);
      }
    },
    methods: {
      getCustomPosition(position) {
        this.latitude = position.coords.latitude;
        this.longitude = position.coords.longitude;
      },
      async fetchCustomLocationDetails() {
        try {
          const apiKey = 'YOUR_API_KEY';
          const latitude = this.inputLatitude || this.latitude;
          const longitude = this.inputLongitude || this.longitude;
          const apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${encodeURIComponent(
            latitude + ',' + longitude
          )}&key=${apiKey}`;
          const response = await fetch(apiUrl);
          const data = await response.json();
          if (data.results && data.results.length > 0) {
            const location = data.results[0];
            this.foundCustomLocation = location;
            console.log('Custom Location:', location);
            // Lakukan sesuatu dengan data lokasi yang ditemukan
          }
        } catch (error) {
          console.error('Error fetching custom location data:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .custom-location-widget {
    border: 1px solid #c73c3c;
    padding: 20px;
    margin-bottom: 20px;
    text-align: center;
    background-color: #663333;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(43, 97, 48, 0.1);
  }
  
  .custom-location-widget h2 {
    color: #2ab30f;
    font-size: 24px;
    margin-bottom: 20px;
  }
  
  .custom-location-widget p {
    color: #0e0a0a;
  }
  
  .custom-location-widget .location-input {
    margin-top: 20px;
  }
  
  .custom-location-widget .location-input label {
    display: block;
    margin-bottom: 5px;
    color: #2e2958;
    font-size: 16px;
  }
  
  .custom-location-widget .location-input input {
    width: 200px;
    padding: 10px;
    margin-right: 10px;
    border: 1px solid #1b0606;
    border-radius: 4px;
    font-size: 16px;
  }
  
  .custom-location-widget button {
    padding: 10px 20px;
    background-color: #033a05;
    color: rgb(243, 7, 7);
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .custom-location-widget button:hover {
    background-color: #fa0778;
  }
  
  .custom-location-widget button:disabled {
    background-color: #240101;
    color: #05fafa;
    cursor: not-allowed;
  }
  
  .custom-location-widget .location-details {
    margin-top: 20px;
    text-align: left;
  }
  
  .custom-location-widget .location-details h3 {
    margin-bottom: 10px;
    color: #09fc1d;
    font-size: 18px;
  }
  
  .custom-location-widget .location-details p {
    margin: 5px 0;
    color: #5605ee;
  }
  
  .custom-location-widget .error-message {
    color: blue;
    margin-top: 10px;
  }
  </style>
  