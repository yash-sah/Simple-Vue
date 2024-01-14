<template>
    <div>
      <h2>Weather Widget</h2>
      <div v-if="weather" @mouseover="showDetails = true" @mouseout="showDetails = false">
        <p>Weather Code: {{ weather.description }}</p>
        <p>Temperature: {{ weather.temperature }}°C</p>
        <p style="color: blue;font-style: italic;" v-if="showDetails">Extra Information: <br>
            Humidity: {{ weather.humidity }} <br>
            Visibility: {{ weather.visibility }}
        </p>
        
      </div>
      

      <p v-else>Loading weather...</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        weather: null,
        showDetails:false,
      };
    },
    mounted() {
      this.getLocation();
    },
    methods: {
      async getLocation() {
        try {
          // Get user's geolocation
          navigator.geolocation.getCurrentPosition(
            (position) => {
              const { latitude, longitude } = position.coords;
              this.fetchWeather(latitude, longitude);
            },
            (error) => {
              console.error('Error getting geolocation:', error);
            }
          );
        } catch (error) {
          console.error('Error getting geolocation:', error);
        }
      },
      async fetchWeather() {
        try {
          const response = await this.$axios.get('https://api.tomorrow.io/v4/weather/forecast?location=Boston&apikey=BxEPGLMrgy2xUBYzFmcMnkRTke0Gv0og', {
          });
          this.weather = {
            temperature: response.data.timelines.minutely[0].values.temperature,
            description: response.data.timelines.minutely[0].values.weatherCode,
            humidity: response.data.timelines.minutely[0].values.humidity,
            visibility:response.data.timelines.minutely[0].values.visibility,
          };
        } catch (error) {
          console.error('Error fetching weather:', error.response || error.message || error);
        }
      },
    },
  };
  </script>