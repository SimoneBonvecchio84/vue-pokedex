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
    <input v-model="pokemonName" type="text">
    <button @click="$emit('printPokemon')">Ottieni Pokemon</button>
</template>