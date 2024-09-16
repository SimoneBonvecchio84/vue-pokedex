<script>
export default {
    props: {
        capturedPokemon: {
            type: Array,
            default: () => []
        }
    }
};
</script>

<template>
    <div class="cont-capt">
        <h3 class="text-center">Pokémon Catturati</h3>
        <ul class="text-center">
            <li class="fs-5 text-light" v-for="poke in capturedPokemon" :key="poke.id">
                {{ poke.name }}
            </li>
        </ul>
        
    </div>
</template>

<style>
.cont-capt{
    height:631px;
}
</style>