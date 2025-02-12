<template>
  <v-container max-width="700">
    <!-- Données de l'exercice -->
    <exercice-objectifs number="6"/>
    <!-- Zone de travail pour l'exercice -->
    <div class="exe-zone">
      <h2>Zone d'exercice</h2>
      <v-btn @click="tasks = []">Effacer les tâches</v-btn>
      <v-card
        class="mx-auto my-6 pa-2"
        max-width="500"
      >
        <v-text-field
          label="Nouvelle tâche"
          clearable
          v-model="newTask"
          @keydown.enter="addTask"
        >
          <template v-slot:append-inner>
            <v-btn @click="addTask">Ajouter</v-btn>
          </template>
        </v-text-field>

        <v-card-title>Liste des tâches</v-card-title>

        <v-card-subtitle v-if="tasks.length < 1">
          Il n'y a pas de tâches... chanceux ! 😄
        </v-card-subtitle>

        <v-list>
          <v-list-item v-for="t in sortTasks" :key="t.date">
            <template v-slot:prepend>
              <v-list-item-action start>
                <v-checkbox-btn v-model="t.completed" />
              </v-list-item-action>
            </template>

            <v-list-item-title :class="{ done: t.completed }">
              {{ t.title }}
            </v-list-item-title>

            <v-list-item-subtitle>
              Créé le {{ new Date(t.date).toLocaleDateString() }}
              à {{ new Date(t.date).toLocaleTimeString() }}
            </v-list-item-subtitle>
          </v-list-item>
        </v-list>
      </v-card>
    </div>
  </v-container>
</template>

<script setup>
// Importation du composant ExerciceObjectifs
import ExerciceObjectifs from "@/components/ExerciceObjectifs.vue";
// Importation de la fonction réactive ref
import {computed, ref, watch} from 'vue';

// Tableau réactif de tâches
const tasks = ref([
  {
    "title": "Acheter du Lait",
    "completed": false,
    "date": 1738162351961
  },
  {
    "title": "Nettoyer le four",
    "completed": false,
    "date": 1737978751912
  },
  {
    "title": "Acheter de l'aspirine",
    "completed": true,
    "date": 1737856351933
  }
]);
// Nouvelle tâche à ajouter
const newTask = ref("");

// Propriété calculée qui trie les tâches par date de création
const sortTasks = computed(function () {
  // Créer un nouveau tableau trié par date de création
  return [...tasks.value].sort((a, b) => b.date - a.date)
})

/**
 * Fonction qui ajoute une nouvelle tâche à la liste.
 */
function addTask () {
  // Ajout de la nouvelle tâche
  tasks.value.push({
    "title": newTask.value,
    "completed": false,
    "date": Date.now() // Date actuelle au format timestamp
  });
  // Réinitialisation de la saisie
  newTask.value = "";
}

// Watcher qui supprime les tâces si on écrit "delete" dans le champ de saisie
watch(newTask, (newVal, OldVal) => {
  console.log('new:', newVal, 'old:', OldVal)
  if (newVal.toLowerCase() === 'delete') {
    tasks.value = []; // Efface toutes les tâches
    newTask.value = ''; // Réinitialise le champ de saisie
  }
})


</script>

<style scoped lang="css">
.done {
  text-decoration: line-through;
}
</style>
