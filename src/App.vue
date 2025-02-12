<template>
  <form action="" @submit.prevent="ajouterTache(newTache)">
    <input type="text" placeholder="Ajouter une tache" v-model="newTache" />
    <button :disabled="newTache.length === 0">Ajouter</button>
  </form>

  <ul v-if="taches.length !== 0">
    <li
      v-for="tache in sortedTodos()"
      :key="tache.date"
      :class="{ completed: tache.isDone }"
    >
      <label>
        <input type="checkbox" v-model="tache.isDone" />
        {{ tache.title }}
      </label>
    </li>
  </ul>
  <h1 v-else>Pas de taches</h1>
  <label>
    <input type="checkbox" v-model="isHidden" />
    Masquer les taches terminées
  </label>
</template>

<script setup>
import { ref } from "vue";

const isHidden = ref(false);

const taches = ref([
  {
    title: "Faire les courses",
    date: Date.now(),
    isDone: false,
  },
]);

const newTache = ref("");

const ajouterTache = (tache) => {
  taches.value.push({
    title: tache,
    date: Date.now(),
    isDone: false,
  });
};

const sortedTodos = () => {
  const sortedTodos = taches.value.sort((a, b) =>
    a.isDone > b.isDone ? 1 : -1
  );
  if (isHidden.value === true) {
    return sortedTodos.filter((tache) => tache.isDone === false);
  }
  return sortedTodos;
};
</script>

<style>
.completed {
  opacity: 0.5;
  text-decoration: line-through;
}
</style>
