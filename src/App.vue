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
      this.capturePokemon();
      
    },
    capturePokemon() {
      if (this.pokemon && !this.capturedPokemon.find(p => p.name === this.pokemon.name)) {
        this.capturedPokemon.push(this.pokemon);
        localStorage.setItem("capturedPokemon", JSON.stringify(this.capturedPokemon)); // Salva nel localStorage
      }
    },
    freePokemon() {
      localStorage.clear();
      // window.location.reload()
      this.capturedPokemon = [];
      console.log(localStorage)

    }
  }
};
</script>

<template>
  <div class="container-big">
    <AppHeader v-model="pokemonName" 
    @printPokemon="printPokemon" 
    @capturePokemon="capturePokemon"
    @freePokemon="freePokemon"
    />
    <div class="container">
      <div class="row p-1">
        <div class="col-6">
          <div class="cont-stat">
            <AppCard v-if="pokemon" :pokemon="pokemon" />
            <div v-else>
              <p>Nessun Pokémon selezionato.</p>
            </div>
          </div>
          <div>
            
          </div>
        </div>
        <div class="col-6">
          <div class="cont-chatc">
            <AppCapturePokemon v-if="capturedPokemon" :capturedPokemon="capturedPokemon" @click="freePokemon"/>
            <div v-else>
              <p>Nessun Pokémon Catturato.</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<style>
body {
  background-color: beige;
}
.cont-stat, .cont-chatc {
  border: solid 2px ;
  border-radius: 8px;
  padding: 10px;
  background-color: darkgreen;
}

</style>