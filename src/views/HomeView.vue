<template>
  <div class="container">
    <h1 class="text-center mt-5">Vue Weather API TS</h1>
    <p class="text-center">Météo en temps réel</p>
    <br />
    <form @submit.prevent="getWeatherInfo(city)">
      <input
        type="text"
        v-model="city"
        class="form-control input mx-auto"
        placeholder="Entrez une ville"
      />
      <br />
      <div class="text-center">
        <button type="submit" class="btn btn-success">Rechercher</button>
      </div>
    </form>
    <div v-if="loader" class="text-center mt-5">
      <div class="spinner-border" role="status">
      </div>
      <span class="ms-3">Chargements des données ...</span>
    </div>
    <weather-results v-if="results && !loader" :results="results" />
    <h2 v-if="error_mess && !loader" class="text-danger text-center mt-4">
      {{ error_mess }}
    </h2>
  </div>
</template>

<script lang="ts">
import WeatherResults from "@/components/WeatherResults.vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "HomeView",
  components: {
    WeatherResults,
  },
  data() {
    return {
      city: "" as string,
      results: null as null | string,
      error_mess: null as null | string,
      loader: false as boolean
    };
  },
  methods: {
    async getWeatherInfo(city: string) {
      // Active l'overlay
      this.loader = true

      // sleep
      await new Promise(r => setTimeout(r, 1000));
      
      // URL de l'API à consommer
      const url =
        "https://api.openweathermap.org/data/2.5/weather?q=" +
        city +
        "&units=metric" +
        "&appid=" +
        process.env.VUE_APP_WEATHER_API_KEY;
      //console.log(city);

      // Consommation de l'API avec la méthode fetch
      await fetch(url).then(async (response) => {
        // Si status code = 200
        if (response.status === 200) {
          this.error_mess = null;
          this.results = await response.json();
        // Sinon on affiche l'erreur à l'utilisateur
        } else if (response.status === 404) {
          this.results = null
          this.error_mess = "La ville renseignée est incorrecte.";
        }
      });
      this.loader = false
    },
  },
});
</script>

<style scoped>
.container {
  max-width: 750px;
}

.input {
  max-width: 600px;
}
</style>