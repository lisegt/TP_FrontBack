<template>
  <div>
    <table class="table table-bordered table-sm table-hover">
      <thead>
        <tr>
          <th>Nom</th>
          <th>Population</th>
          <th>Action</th>        
        </tr>
      </thead>
      <tbody>
        <tr v-for="city in cities" :key="city.id"> 
          <td>{{ city.name }}</td>
          <td>{{ city.population }}</td>
          <td><button @click="$emit('delete', city._links.self.href)">Supprimer</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const props = defineProps({
  cities: {
    type: Array,
    required: true,
  },
});



</script>

<style>

</style>