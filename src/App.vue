<template>
  <body v-if="!fin">
    <h1>Questionnaire sur les Films et Séries</h1>
    <ProgressBare :remplissage="remplissageValue"></ProgressBare>
    <Question
      :numéro="numQuestion"
      :fin="fin"
      @update:fin="fin = $event"
      @update:numQuestion="numQuestion = $event"
      @update:remplissageValue="remplissageValue = $event"
      @update:score="score += 1"
    />
  </body>
  <body v-else>
    <h1>Fin du questionnaire</h1>
    <p>Vous avez {{ score }}/5</p>
  </body>
</template>

<script setup>
import ProgressBare from "/src/Quiz/ProgressBarre.vue";
import { ref } from "vue";
import Question from "/src/Quiz/Question.vue";

const numQuestion = ref(1);
const fin = ref(false);
const score = ref(0);
const remplissageValue = ref(0);
</script>
