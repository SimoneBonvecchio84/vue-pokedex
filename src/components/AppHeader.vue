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
  <nav class="navbar ">
    <div class="container">
      <a class="navbar-brand">Pokemon Hunter</a>
      <div class="d-flex px-3 align-items-center" role="search">
        <input v-model="pokemonName" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
        <button @click="$emit('printPokemon')" class="btn btn-outline-light me-2" type="submit">Vedi Pokemon</button> 
        <a @click="$emit('capturePokemon')"  type="btn"><img class="img-btn" src="../assets/img/pokeball.jpg" alt=""></a>    
      </div>
    </div>
  </nav>
</template>

<style>
.navbar{
  background-color: darkgreen;
  border: 2px solid;
}
.form-control{
  background-color: beige;
}
.img-btn{
  width: 60px;
  border-radius: 50%;
  cursor: pointer;
}

.img-btn:hover{
  opacity: 70%;
}
</style>