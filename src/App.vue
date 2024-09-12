<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
export default {
  components: {
    AppHeader
  },
  data() {
    return {
      pokemon: {}
    }
  },
  methods : {
     printPokemon() {
       axios.get("https://pokeapi.co/api/v2/pokemon/caterpie").then((resp) => {
        console.log(resp); 
        this.pokemon = resp;
       });
     }
  }

}
</script>
<template>
  <AppHeader/>
  <button @click="printPokemon">Ottieni Pokemon</button>
  <div>{{ pokemon.abilities }}</div>
  <div>

  </div>
</template>