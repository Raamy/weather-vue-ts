<template>
  <div class="mt-4" v-if="results">
    <h1>Informations météo pour :</h1>
    <h2 class="mt-2">{{ results.name + ", " + results.sys.country }}</h2>
    <p>Date de réception des données : {{ new Date(results.dt * 1000).toLocaleString() }}</p>
    <hr />
    <h3>Température : {{ results.main.temp }}°C</h3>
    <h3>Météo : {{ results.weather[0].main }}</h3>
    <h3>Taux d'humidité : {{ results.main.humidity }} %</h3>
    <br/>
    <h3>Temp. minimale : {{ results.main.temp_min }} °C</h3>
    <h3>Temp. maximale : {{ results.main.temp_max }} °C</h3>
    <br/>
    <h3>Lever de soleil : {{ new Date(results.sys.sunrise * 1000).toLocaleString() }}</h3>
    <h3>Coucher de soleil : {{ new Date(results.sys.sunset * 1000).toLocaleString() }}</h3>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "WeatherResults",
  props: {
    results: String,
  }
});
</script>