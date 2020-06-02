<template>
  <div>
    <h1>Offlinewecker</h1>
    <PluginList></PluginList>
    <input
      style="max-width: 230px; width: 100%"
      @keyup.enter="searchWeather"
      placeholder="Wetter nach Stadtname suchen"
      v-model="city"
    />

    <h1>Wetterdaten</h1>
    <table style="margin: auto">
      <tr>
        <th>Stadt</th>
        <th>Windstärke</th>
        <th>Bewölkerung</th>
        <th>Luftfeuchtigkeit</th>
      </tr>
      <tr v-for="(weatherData, index) in weatherArray" :key="index">
        <td>
          {{ weatherData.name }}
        </td>
        <td>
          {{ weatherData.wind.speed }}
        </td>
        <td>{{ weatherData.clouds.all }}%</td>
        <td>{{ weatherData.main.humidity }}%</td>
      </tr>
    </table>
  </div>
</template>

<script>
import PluginList from "@/components/PluginList.vue";
// import Timer from "@/components/Timer.vue";
// import Weather from "@/components/Weather.vue";

export default {
  name: "Home",
  components: {
    PluginList
    // Weather
  },
  data() {
    return {
      openWeather: "28d120b80a2d5628d3346dcf1c1cdc2b",
      city: "",
      weatherArray: []
    };
  },
  methods: {
    searchWeather() {
      this.axios
        .get(
          "HTTP://api.openweathermap.org/data/2.5/weather?q=" +
            this.city +
            "&appid=" +
            this.openWeather
        )
        .then(response => {
          this.weatherArray.push(response.data);
        });
    }
  }
};
</script>
