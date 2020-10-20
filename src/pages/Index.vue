<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input v-model="text" placeholder="Search" borderless dark>
        <template v-slot:before>
          <q-icon @click="getLocation" name="my_location" />
        </template>

        <template v-slot:hint> Field hint </template>

        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div>

    <template v-if="weatherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">Abuja</div>
        <div class="text-h6 text-weight-light">Rain</div>
        <div class="text-h1 text-weight-thin q-my-lg relative-position">
          <span>8</span>
          <span class="text-h4 relative-position degree">&deg;c</span>
        </div>
      </div>

      <div class="col text-center">
        <img src="https://www.fillmurray.com/100/100" alt="weather Image" />
      </div>
    </template>
    <template v-else>
      <div class="col column text-center text-white">
        <div class="col text-h2 text-weight-thin">Quasar<br />Weather</div>
        <q-btn @click="getLocation" class="col" flat>
          <q-icon left size="3em" name="my_location" />
          <div>Find my Location</div>
        </q-btn>
      </div>
    </template>

    <div class="col skyline"></div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      search: "",
      weatherData: null,
      lat: null,
      lon: null,
      apiUrl: "https://api.openweathermap.org/data/2.5/weather",
      apiKey: "eb81bd807906e1932e4d5da87a6fa9c3",
    };
  },
  methods: {
    getLocation() {
      navigator.geolocation.getCurrentPosition((position) => {
        this.lat = position.coords.latitude;
        this.lon = position.coords.longitude;
        this.getWeatherByCoords();
      });
    },
    getWeatherByCoords() {
      this.axios(
        `${this.apiUrl}?lat=${this.lat}&lon=${this.lon}&appid=${this.apiKey}`
      );
    },
  },
};
</script>

<style lang="sass">
.q-page
  background: linear-gradient(to bottom, #136a8a, #267871)
.degree
  top: -44px
.skyline
  flex: 0 0 100px
  background: url(../assets/skyline.png)
  background-size: contain
  background-position: center bottom
</style>
