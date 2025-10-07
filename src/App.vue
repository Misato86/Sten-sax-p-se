<script setup>
import { ref } from 'vue';
import Knapprad from './components/icons/KnappRad.vue';
import ResultatRad from './components/ResultatRad.vue';

const knappar = ref(['Sten', 'Sax', 'Påse']);
const score = ref({spelare: 0, dator: 0});
const resultat = ref({});
const vinnare = ref('');



function hittaVinnare(valdaKnappar) {
  let spelare = knappar.value.indexOf(valdaKnappar.spelare)
  let dator = knappar.value.indexOf(valdaKnappar.dator)
  resultat.value = { spelare: spelare, dator: dator }

}

function raknaPoang(v) {
  if(v === 'spelare') {
    score.value.spelare ++
  } else {
    score.value.dator ++
  }
  
  vinnare.value = v
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
    <knapprad :knappar="knappar" @valda-knappar="hittaVinnare"/>

    <ResultatRad :valdaKnappar="resultat" @vinnare="raknaPoang"/>

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
