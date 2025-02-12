<template>
  <div>
    <h2>{{ intitulés[numéro - 1] }}</h2>

    <ul>
      <li v-for="(réponse, index) in réponses[numéro - 1]" :key="index">
        <input
          type="radio"
          :id="`q${numéro}-${index}`"
          :name="`q${numéro}`"
          :value="réponse"
          v-model="réponseSelectionnée"
        />

        <label :for="`q${numéro}-${index}`">{{ réponse }}</label>
      </li>
    </ul>
    <div class="button">
      <button @click="suivant">Question suivante</button>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from "vue";

const { fin, numéro } = defineProps({
  numéro: {
    type: Number,
    required: true,
  },
  fin: {
    type: Boolean,
    required: true,
  },
});

// Emission d'événements
const emit = defineEmits([
  "update:numQuestion",
  "update:fin",
  "update:remplissageValue",
  "update:score",
]);

const numQuestion = ref(1);

const intitulés = [
  "Qui est le roi de france",
  "Trouve le 2",
  "2+5",
  "1+1",
  "1+2",
];

const réponses = [
  ["Machin", "truc", "Macron", "Brigitte"],
  ["1", "2", "3", "4"],
  ["1", "2", "3", "7"],
  ["1", "2", "3", "7"],
  ["1", "2", "3", "7"],
];

const vrai = ["Macron", "2", "7", "2", "3"];

const réponseSelectionnée = ref(null);

const suivant = () => {
  if (réponseSelectionnée.value === vrai[numQuestion.value - 1]) {
    emit("update:score", 1);
  }

  if (numQuestion.value < 5) {
    numQuestion.value++;
    augmenter();
    emit("update:numQuestion", numQuestion.value);
    réponseSelectionnée.value = null;
  } else {
    emit("update:fin", true);
  }
};

const remplissageValue = ref(0);

const augmenter = () => {
  if (remplissageValue.value < 100) {
    remplissageValue.value += 25;
    emit("update:remplissageValue", remplissageValue.value);
  }
};
</script>

<style>
.button {
  display: flex;
  justify-content: center;
  align-items: end;
  flex-direction: column;
  padding: 20px;
  gap: 20px;
}
</style>
