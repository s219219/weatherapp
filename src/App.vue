<!-- Html template of thr project -->
<template>
  <div id="app">
    <main>
      <div class="search-box">
        <label for="search">
          <h2>A Simple <u>weather application</u>.<br>Put here City or a country 🌤️</h2>
        </label><br>
        <p style="margin-top: 0px !important; margin-bottom: 25px;">
          Project was done on Vue.js using
          <a href="https://openweathermap.org/weathermap" target="_blank"> Open Weather Map API</a>
          and shows the current weather
        </p>
        <!-- From input writing data to a variable -->
        <input type="text" id="search" class="search-bar" placeholder="Search..." v-model="query" @keypress="fetchWeather"/>
      </div>
      <!-- Show only if something is found -->
      <div class="weather-container" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <center>
            <div class="weather-img">
              <!-- Show weather image from array -->
              <img v-bind:src="'http://openweathermap.org/img/w/' + weather.weather[0].icon + '.png'">
            </div>
          </center>
          <!-- Show location and country symbols -->
          <div class="location"><b>Location:</b> {{ weather.name }}, {{ weather.sys.country }}</div>
          <!-- Show date from function -->
          <div class="date"><b>Date:</b> {{ dateBuilder() }}</div>
        </div>
        <div class="weather-box">
          <!-- Show temperature -->
          <div class="temp"><b>Temperature:</b> {{ Math.round(weather.main.temp) }}°c</div>
          <!-- Show weather -->
          <div class="weather"><b>Weather:</b> {{ weather.weather[0].main }}, {{ weather.weather[0].description}}</div>
        </div>
      </div>
    </main>
  </div>
</template>
<!-- Html template of thr project -->

<script>

export default {
  name: 'app',
  data () {
    return {
      api: '599582fd748f4514a98d3013365e1e32', // API from an aplication
      query: '', // query from input
      weather: {} // list of data
    }
  },
  methods: {
    fetchWeather (e) {
      this.c = true;
      if (e.key == "Enter") { // If button enter was pressed
        // asking for data through API
        fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.query}&units=metric&APPID=${this.api}`)
          .then(res => {
            return res.json(); //getting Json data
          }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results; //giving data to list
    },
    dateBuilder () { //function of bulding beautiful date
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>
