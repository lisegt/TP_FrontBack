<template>


  <div class="home">
    <h2>Villes par pays</h2>
    <div class="row">
        <label for="country">Pays:</label>
            <select class="form-control">
                <option disabled value="0" selected>Choisissez un pays</option>
                <option v-for="country in data.countries" :key="country.id" :value="country._links.cities.href">
                {{ country.name }}
              </option>
            </select>
    </div>
    <hr/>
    <div class="row">
    </div>   
  </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";

let data = reactive({
  countries: []
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

// Au chargement du composant
onMounted(() => {
  fetchCountries(); // On récupère les pays (pour le sélecteur de pays)
}); 

</script>


<style>

</style>