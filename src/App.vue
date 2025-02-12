<template>
  <Layout>
    <template #header> En tête </template>
    <template #aside>aside</template>
    <template #main>main</template>
    <template #footer>footer</template>
  </Layout>
  <form action="" @submit.prevent="ajouterTache(newTache)">
    <input type="text" placeholder="Ajouter une tache" v-model="newTache" />
    <button :disabled="newTache.length === 0">Ajouter</button>
  </form>

  <ul v-if="taches.length !== 0">
    <li
      v-for="tache in sortedTodos"
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
  <Checkbox
    label="Masquer les composants terminés"
    @check="console.log('checked')"
    @uncheck="console.log('unchecked')"
    v-model="isHidden"
  />

  <Checkbox
    label="Bonjour"
    @check="console.log('checked')"
    @uncheck="console.log('unchecked')"
  />
</template>

<script setup>
import { computed, ref } from "vue";
import Checkbox from "/src/Checkbox.vue";
import Button from "/src/Button.vue";
import Layout from "./Layout.vue";

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

const sortedTodos = computed(() => {
  const sorted = [...taches.value].sort((a, b) =>
    a.isDone > b.isDone ? 1 : -1
  );
  if (isHidden.value) {
    return sorted.filter((tache) => !tache.isDone);
  }
  return sorted;
});
</script>

<style>
.completed {
  opacity: 0.5;
  text-decoration: line-through;
}
</style>
