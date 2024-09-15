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
        <h3 class="text-center">Pokémon Catturati</h3>
        <ul class="text-center">
            <li class="fs-5" v-for="poke in capturedPokemon" :key="poke.id">
                {{ poke.name }}
            </li>
        </ul>
    </div>
</template>