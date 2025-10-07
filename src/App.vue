<script setup>
import { ref } from 'vue';
import Knapprad from './components/icons/KnappRad.vue';

const knappar = ref(['Sten', 'Sax', 'Påse']);
const score = ref({spelare: 0, dator: 0});
const resultat = ref('Du vann!');



function hittaVinnare(knappar) {

    if(knappar.spelare === knappar.dator) {
        resultat.value = "Oavgjort!"
      } else if(
        (knappar.spelare == "Sten" && knappar.dator == "Sax") ||
        (knappar.spelare == "Sax" && knappar.dator == "Påse") ||
        (knappar.spelare == "Påse" && knappar.dator == "Sten")
      ) {
        resultat.value = "Du vann!"
        score.value.spelare++
      } else {
        resultat.value = "Du förlorade!"
        score.value.dator++
    }
}

function reset() {
  score.value.spelare = 0
  score.value.dator = 0
  let buttons = document.getElementsByClassName('alternativ')
    for (let b of buttons) {
       b.classList.remove('spelarval')
       b.classList.remove('datorval')
    }
}


</script>

<template>
  <header>
    <h1>Sten, sax, påse!</h1>

  </header>

  <main>
    <knapprad :knappar = "knappar" @valda-knappar="hittaVinnare"/>

    <div class="resultat">
      <p id="resultat">{{ resultat }}</p>
    </div>

    <div class="score">
      <button id="nolla" @click="reset" >Nollställ poäng</button>
      <p>
        <span id="spelare">{{ score.spelare }}</span> -
        <span id="dator">{{ score.dator }}</span>
      </p>
    </div>
  </main>
</template>

<style scoped>
  header {
    text-align: center;
    margin-bottom: 1,2em;
  }
  .resultat {
    text-align: center;
    font-size: 1.2em;
    margin: 1,2em 0;
  }
  .score {
    text-align: center;
    font-size: 1.2em;

  }
  #nolla {
    margin-top: 2em;
    padding: .3em .6em;
    font-size: .8em;
  }
</style>
