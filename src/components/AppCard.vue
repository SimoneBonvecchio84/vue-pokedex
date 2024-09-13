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
    <div>
        <img :src="pokemon.sprites.front_default" alt="">
    </div>
    <div class="pokemon-card">
      <div>Name: {{ pokemon.name }}</div>
      <ul>
        <li v-for="(curType) in pokemon.types">
        Type: {{ curType.type.name }}
        </li>
      </ul>
      <div>Height: {{ pokemon.height }}" </div>
      <div>Weight: {{ pokemon.weight }} Ibs.</div>
        
    
    </div>

    <div>
        <div>Status</div>
        <ul>
            <li v-for="(curStat) in pokemon.stats">
                {{ curStat.stat.name }} <span> {{ curStat.base_stat }} </span> 
            </li>
        </ul>
    </div>
  </template>