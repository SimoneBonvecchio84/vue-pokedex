<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import { store } from './store';
export default {
  components: {
    AppHeader
  },
  data() {
    return {
      store
    }
  },
  methods : {
     printPokemon() {
       const searchPokemon = `https://pokeapi.co/api/v2/pokemon/${this.store.pokemonName}`
       axios.get(searchPokemon).then((resp) => {
        console.log(resp); 
        this.store.pokemon = resp.data;
        
       });
     }
  }

}
</script>
<template>
  <AppHeader @printPokemon="printPokemon"/>

  

  
  <!-- <div class="d-flex justify-content-center mt-5">
    <div class="card" style="width: 18rem;"> -->
  <!-- <ul class="list-group list-group-flush">
    <div v-if="(pokemon.sprites.front_default !== null)">
      <img :src="pokemon.sprites.front_default" alt="">
    </div>
    <div v-else>
        <span>Immagine non presente</span>
    </div> -->
    <!-- <li class="list-group-item"> Name:{{ pokemon.name }}</li>
    <li v-for="(type) in pokemon.types" class="list-group-item">
      Type: {{ type.type.name }}
    </li>
    <li class="list-group-item">
      Height: {{ pokemon.height }} "
    </li>
    <li class="list-group-item">
      Weight: {{ pokemon.weight }} Ibs
    </li> -->

   <!-- <div>
     <ul>
      <li v-for="(curStat) in pokemon.stats" >
        {{ curStat.stat.name }} {{ curStat.base_stat }}
      </li>
     </ul>
   </div>
</div> -->
  <!-- </div> -->
</template>