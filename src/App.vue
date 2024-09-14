<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppCard from './components/AppCard.vue';
import AppCapturePokemon from './components/AppCapturePokemon.vue';

export default {
  components: {
    AppHeader,
    AppCard,
    AppCapturePokemon
  },
  data() {
    return {
      pokemonName: "",
      pokemon: null,
      capturedPokemon: [] // Aggiungi un array per i Pokémon catturati
    };
  },
  created() {
    // Recupera i Pokémon salvati dal localStorage quando il componente viene montato
    const savedPokemon = localStorage.getItem("capturedPokemon");
    if (savedPokemon) {
      this.capturedPokemon = JSON.parse(savedPokemon);
    }
  },
  methods: {
    printPokemon() {
      const searchPokemon = `https://pokeapi.co/api/v2/pokemon/${this.pokemonName.toLowerCase()}`;
      axios.get(searchPokemon).then((resp) => {
        console.log(resp);
        this.pokemon = resp.data;
      }).catch((err) => {
        console.error("Pokémon non trovato", err);
        this.pokemon = null;  // Pulisce i dati precedenti in caso di errore
      });
      this.capturePokemon()
    },
    capturePokemon() {
      if (this.pokemon && !this.capturedPokemon.find(p => p.name === this.pokemon.name)) {
        this.capturedPokemon.push(this.pokemon);
        localStorage.setItem("capturedPokemon", JSON.stringify(this.capturedPokemon)); // Salva nel localStorage
      }
    }
  }
};
</script>

<template>
  <div class="container">
    <AppHeader v-model="pokemonName" @printPokemon="printPokemon" @click="capturePokemon" />
    <div>

      <AppCard v-if="pokemon" :pokemon="pokemon" /> 
      <div v-else>
        <p>Nessun Pokémon selezionato.</p>
      </div>
      <AppCapturePokemon v-if="capturedPokemon" :capturedPokemon="capturedPokemon" />
      <div v-else>
        <p>Nessun Pokémon Catturato.</p>
      </div>
    </div>
  </div>
</template>


<style>

</style>