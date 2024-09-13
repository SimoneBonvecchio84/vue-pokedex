<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppCard from './components/AppCard.vue';

export default {
  components: {
    AppHeader,
    AppCard
  },
  data() {
    return {
      pokemonName: "",
      pokemon: null
    };
  },
  methods: {
    printPokemon() {
      const searchPokemon = `https://pokeapi.co/api/v2/pokemon/${this.pokemonName.toLocaleLowerCase()}`;
      axios.get(searchPokemon).then((resp) => {
        console.log(resp);
        this.pokemon = resp.data;
      }).catch((err) => {
        console.error("Pokémon non trovato", err);
        this.pokemon = null;  // Pulisce i dati precedenti in caso di errore
      });
    }
  }
};
</script>
<template>
  <div>
    <AppHeader v-model="pokemonName" @printPokemon="printPokemon" />
    <div >
      <AppCard v-if ="pokemon" :pokemon="pokemon" /> 
     
      <div v-else>
        <p>Nessun Pokémon selezionato.</p>
      </div>
    </div>
  </div>
</template>