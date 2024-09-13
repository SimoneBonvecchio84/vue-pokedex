<script>
export default {
  props: {
    pokemon: {
      type: Object,
      required: true
    }
  }
};
</script>

<template>
    <div class="pokemon-card">
      <h3>{{ pokemon.name }}</h3>
      <p>Altezza: {{ pokemon.height }}</p>
      <p>Peso: {{ pokemon.weight }}</p>
    </div>
  </template>