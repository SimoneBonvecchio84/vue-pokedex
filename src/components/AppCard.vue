<script>
export default {
    props: {
        pokemon: {
            type: Object,
            required: true
        }
    },
    methods: {
        statBar(value) {
            const maxValueBar = 250;
            return (value / maxValueBar) * 100;
        }
    }
};
</script>

<template>
    <div class="container-img">
        <img :src="pokemon.sprites.front_default" alt="">
        <img :src="pokemon.sprites.back_default" alt="">
    </div>
    <div class="pokemon-card">
        <div>Name: {{ pokemon.name }}</div>
        <ul>
            <li class="li-type" v-for="(curType) in pokemon.types">
                Type: {{ curType.type.name }}
            </li>
        </ul>
       
        
        <div>Height: {{ pokemon.height }}" </div>
        <div>Weight: {{ pokemon.weight }} Ibs.</div>


    </div>

    <div>
        <div>Status</div>
        <ul>
            <li v-for="(curStat) in pokemon.stats" class="d-flex">
                <div class="stat-name">
                    {{ curStat.stat.name }} :
                </div>
                
                <div class="stat-bar">
                    <div class="stat-bar-fill" :style="{ width: statBar(curStat.base_stat) + '%' }"></div>
                </div>
            </li>


        </ul>
    </div>
</template>
<style scoped>
ul {
    list-style-type: none;
    margin-top: 20px;
}

.li-type{
    margin-left: -30px;
}

.container-img{
    margin-top: 20px;
}

.pokemon-card {
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 8px;
  max-width: 300px;
  margin-bottom: 20px;
  margin-top: 20px;
}
.stat-name {
    width: 10%;
    margin-left: -30px;
}
.stat-bar {
  width: 20%;
  background-color: #eee;
  height: 10px;
  margin: 5px 0;
  position: relative;
}

.stat-bar-fill {
  background-color:black; /* Colore della barra riempita */
  height: 100%;
  transition: width 0.3s ease; /* Transizione per un effetto fluido */
}
</style>