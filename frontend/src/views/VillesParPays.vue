<template>


  <div class="home">
    <h2>Villes par pays</h2>
    <div class="row">
        <label for="country">Pays:</label>
            <select id="countrySelector" class="form-control" @change="fetchCities">
                <option disabled value="0" selected>Choisissez un pays</option>
                <option v-for="country in data.countries" :key="country.id" :value="country._links.cities.href">
                {{ country.name }}
              </option>
            </select>
    </div>
    <hr/>
    <div class="row">
      <VillesParPaysList :cities="data.cities" @delete="deleteCity"/>
    </div>   
  </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";
// @ is an alias to /src
import VillesParPaysList from "@/components/VillesParPaysList.vue";

let data = reactive({
  countries: [],
  cities: []
});

// Utilise l'API REST auto-générée pour récupérer les pays
function fetchCountries() {
  fetch("api/countries")
    .then((response) => response.json())
    .then((json) => {
      data.countries = json._embedded.countries;
    })
    .catch((error) => alert(error));
}

// récupérer les villes
function fetchCities() { //link : url des villes appartenant au pays sélectionné
  // Utilise l'API ad-hoc pour avoir le pays de chaque ville
  let link = document.getElementById('countrySelector').value
  fetch(link)
    .then((response) => response.json())
    .then((json) => {
      data.cities = json._embedded.cities;
    })
    .catch((error) => alert(error));
}

//supprimer une ville
function deleteCity(link) { //link : url de la ville à supprimer
  console.log(link)
  fetch(link, {method: "DELETE"})
    .then((response) => { fetchCities();})
    .catch((error) => console.log(error));
    
}

// Au chargement du composant
onMounted(() => {
  fetchCountries(); // On récupère les pays (pour le sélecteur de pays)
}); 

</script>


<style>

</style>