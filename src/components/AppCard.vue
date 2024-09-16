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
            const maxValueBar = 250; // valore numerico massimo
            // calcolo valore in percentuale
            // calcoliamo il valore in percentuale dividendo (value) che poi sarà base_stat
            // per il valore massimo (maxValueBar) e poi moltiplicato * 100 ottenedo così la larghezza della
            // barra in percentuale
            return (value / maxValueBar) * 100; 
        }
    }
};
</script>

<template>
  <div class="cont-left">
    <div class="container-img">
        <img class="img-front" :src="pokemon.sprites.front_default" alt="">
        <img class="img-back" :src="pokemon.sprites.back_default" alt="">
    </div>
    <div class="pokemon-card mt-2  mb-2">
        <div>Name: {{ pokemon.name }}</div>
        <ul>
            <li class="li-type" v-for="(curType) in pokemon.types">
                Type: {{ curType.type.name }}
            </li>
        </ul>
       
        
        <div>Height: {{ pokemon.height }}" </div>
        <div>Weight: {{ pokemon.weight }} Ibs.</div>


    </div>

    <div class="cont-status">
        <div>Status</div>
        <ul>
            <li v-for="(curStat) in pokemon.stats" class="d-flex li-bar">
                <div class="stat-name">
                    {{ curStat.stat.name }} :
                </div>
                <!-- Elemento padre vuoto -->
                <div class="stat-bar">
                     <!--elemento figlio che si riempe di tot % in base al numero restituito da statBar  -->
                    <div class="stat-bar-fill" :style="{ width: statBar(curStat.base_stat) + '%' }"></div>
                </div>
            </li>

        </ul>
    </div>
  </div>
</template>
<style scoped>
.cont-left {
  height:631px;
}
ul {
    list-style-type: none;
    margin-top: 20px;
}

.li-type{
    margin-left: -30px;
}


.container-img{
    margin: auto;
    border: 2px solid;
    border-radius: 8px;
    width: 400px;
    height: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    perspective: 1000px; /* Questo dà un effetto 3D per l'animazione */
    background-color: beige;
}

.img-front, .img-back{
    position: absolute; 
    backface-visibility: hidden; /* Nasconde il resto dell'immagine quando viene ruotata*/
    opacity: 0;
    transition: opacity 1s ease-in-out;
}


/* Anima l'alternanza delle immagini */
@keyframes alternateImages {
  0%, 50% {
    opacity: 1; /* Mostra l'immagine frontale */
  }
  50.01%, 100% {
    opacity: 0; /* Nasconde l'immagine frontale, mostrando quella posteriore */
  }
}

@keyframes alternateBackImages {
  0%, 50% {
    opacity: 0; /* Nasconde l'immagine posteriore all'inizio */
  }
  50.01%, 100% {
    opacity: 1; /* Mostra l'immagine posteriore nella seconda metà dell'animazione */
  }
}

/* Applica l'animazione alle due immagini */
.img-front {
  animation: alternateImages 1s infinite; /* Alternanza per l'immagine frontale */
}

.img-back {
  animation: alternateBackImages 1s infinite; /* Alternanza per l'immagine posteriore */
}

.pokemon-card {
  margin: auto;  
  border: 2px solid;
  padding: 10px;
  border-radius: 8px;
  max-width: 300px;
  background-color: beige;
}

.cont-status {
    border: 2px solid;
    padding: 10px;
    border-radius: 8px;
    background-color: beige;
}
.stat-name {
    width: 30%;
    margin-left: -30px;
}
.stat-bar {
  width: 80%;
  background-color:white;
  border: 1px solid;
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