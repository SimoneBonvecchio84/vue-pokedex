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
    <div>
        <h3>Pokémon Catturati</h3>
        <ul>
            <li v-for="poke in capturedPokemon" :key="poke.id">
                {{ poke.name }}
            </li>
        </ul>
    </div>
</template>