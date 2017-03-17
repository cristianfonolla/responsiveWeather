<template xmlns:v-bind="http://www.w3.org/1999/xhtml">
  <div class="weather">
    <div class="location">{{location}}</div>
    <div class="date">{{date}}</div>
    <div class="description">{{description}}</div>
    <div class="current">
      <div class="visual">
        <div class="icon cloudy" alt="cloudy"></div>
        <div class="temp">{{temp}}</div>
        <div class="scale">ºC</div>
      </div>
      <div class="text">
        <div class="precipitation">Precipitation: {{precipitation}}</div>
        <div class="humidity">Humidity: {{humidity}}</div>
        <div class="wind">Wind: {{wind}}</div>
        <div class="pollen">Pollen: {{pollen}}</div>
      </div>
    </div>
    <div class="forecast">
      <div class="forecast-day" v-for="forecast in forecast">
        <div class="date">{{forecast.date}}</div>
        <div v-bind:class="'icon ' + forecast.icon"></div>
        <div class="forecast-temperature">
          <div class="high-temp">{{forecast.highTemp}}°</div>
          <div class="low-temp">{{forecast.lowTemp}}°</div>
        </div>
        <div class="pcount">Pollen {{pollen}}</div>
      </div>
    </div>
    <md-snackbar md-position="bottom center" ref="connectionError" md-duration="4000">
      <span>Connection error. Ensure the database is open.</span>
    </md-snackbar>
  </div>
</template>

<script>
  export default {
    name: 'weather',
    data () {
      return {
        location: 'Tortosa, ES',
        date: 'Tursday, Abril 2017',
        description: 'Little description here',
        temp: 13,
        precipitation: '75%',
        humidity: '89%',
        wind: '15mph',
        pollen: 50,
        forecast: [
          { 'date': 'Monday', 'icon': 'sunny', 'lowTemp': 5, 'highTemp': 15 },
          { 'date': 'Tuesday', 'icon': 'partly', 'lowTemp': 1, 'highTemp': 10 },
          { 'date': 'Wednesday', 'icon': 'cloudy', 'lowTemp': 2, 'highTemp': 13 },
          { 'date': 'Thursday', 'icon': 'raining', 'lowTemp': -4, 'highTemp': 0 },
          { 'date': 'Friday', 'icon': 'raincloudy', 'lowTemp': 0, 'highTemp': 2 },
          { 'date': 'Saturday', 'icon': 'thunderstorms', 'lowTemp': 1, 'highTemp': 3 },
          { 'date': 'Sunday', 'icon': 'sunny', 'lowTemp': 2, 'highTemp': 10 }
        ]
      }
    },
    methods: {
      fetchWeather: function () {
        console.log('TODO')
      }
    },
    created: function () {
      this.fetchWeather()
    },
    showConnectionError: function () {
      this.$refs.connectionError.open()
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .weather {
    width: 100%;
    display: inline-block;
    padding: 10px 10px 0px 10px;
    box-shadow: 0 1px 4px rgba(0,0,0,0.2);
  }

  @media (min-width: 700px) {
    .weather {
      width: 700px;
    }
  }

  .location {
    font-size: 3em;
    color: black;
  }

  .date {
    color: red;
  }

  .description {
    font-size: 1.1em;
  }

  .current {
    overflow: auto;
    width: 100%;
  }

  .visual {
    float: left;
    width: 50%;
  }

  .visual .icon{
    width: 64px;
    height: 64px;
  }

  .visual .icon.cloudy {
    float: left;
    margin-left: 0;
  }

  .text {
    width: 50%;
    float: right;
  }

  .forecast-day {
    display: inline-block;
    width: 14.285%;
    text-align: center;
  }

  .forecast-day date {
    color: black;
    font-size: 0.5em;
    text-align: center;
    font-weight: bold;
  }

  .forecast-day .icon {
    width: 64px;
    height: 64px;
  }

  .forecast-day .high-temp, .forecast-day .low-temp {
    display: inline-block;
    font-size: 1.25em;
  }

  .forecast-day .low-temp {
    color: rgba(0,0,0,0.4);
  }

  .forecast-day .forecast-temperature {
    text-align: center;
  }

  .icon {
    background-repeat: no-repeat;
    background-size: contain;
    margin-left: auto;
    margin-right: auto;
  }

  .icon.cloudy {
    background-image: url('../assets/cloudy.png');
  }

  .icon.partly {
    background-image: url('../assets/partly_cloudy.png');
  }

  .icon.raining {
    background-image: url('../assets/rain.png');
  }

  .icon.raincloudy {
    background-image: url('../assets/rain_s_cloudy.png');
  }

  .icon.thunderstorms {
    background-image: url('../assets/thunderstorms.png');
  }

  .icon.sunny {
    background-image: url('../assets/sunny.png');
  }

  .visual .temp, .visual .scale, .visual .icon{
    display: inline-block;
  }
  .temp{
    font-size: 2.5em;
  }
  .visual .scale, .visual .temp {
    vertical-align: top;
  }

  .precipitation, .humidity, .wind, .pollen {
    font-size: 0.9em;
    color: #888;
  }

  .current {
    overflow: auto;
    width: 100%;
    margin-bottom: 15px;
  }

  .pcount {
    font-size: 0.9em;
    color: #888;
  }

  @media (max-width: 650px) {
    .location {
      font-size: 5em;
    }

    .forecast-day {
      display: block;
      border-top: 1px solid black;
      width: 100%;
    }

    .forecast-day .date {
      text-align: left;
      font-weight: bold;
      color: black;
    }

    .date, .icon, .high-temp, .low-temp {
      display: inline-block;
    }
  }
</style>