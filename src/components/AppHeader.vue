<script>

export default {
    data() {
        return {
           
        }
    }
}
</script>

<template>

  
<input v-model="pokemonName" type="text">
<button @click="$emit('printPokemon')">Ottieni Pokemon</button>
  
</template>

<style></style>