<script>
export default {
  props: {
    modelValue: String
  },
  computed: {
    pokemonName: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit('update:modelValue', value);
      }
    }
  }
};
</script>

<template>
  
  
  <nav class="navbar bg-body-tertiary">
    <div class="container-fluid">
      <a class="navbar-brand">Pokemon Hunter</a>
      <div class="d-flex" role="search">
        <input v-model="pokemonName" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
        <button @click="$emit('printPokemon')" class="btn btn-outline-danger" type="submit">Vedi Pokemon</button> 
        <button @click="$emit('capturePokemon')" class="btn btn-outline-danger" type="submit">Cattura Pokemon</button>    
      </div>
    </div>
  </nav>
</template>