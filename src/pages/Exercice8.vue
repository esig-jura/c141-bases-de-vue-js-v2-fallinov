<template>
  <v-container max-width="700">
    <!-- Données de l'exercice -->
    <exercice-objectifs number="8"/>
    <!-- Zone de travail pour l'exercice -->
    <div class="exe-zone">
      <h2>Zone d'exercice</h2>

      <!-- Liste des Pokémon -->
      <v-card class="mx-auto my-6 pa-2" max-width="500">
        <v-card-title>Liste des Pokémon</v-card-title>
        <v-card-text>
          <v-list>
            <!-- Element à transformer en composant -->
            <pokemon-card
              v-for="pokeball in pokemons"
              :key="pokeball"
              :poke-nom="pokeball"
              @delete="removePokemon(0)"
            />
            <!-- Fin de l'élément à transformer en composant -->
          </v-list>
        </v-card-text>
      </v-card>
    </div>
  </v-container>
</template>

<script setup>
import { ref } from 'vue';
import ExerciceObjectifs from "@/components/ExerciceObjectifs.vue";
import PokemonCard from "@/components/PokemonCard.vue";

// Liste initiale des Pokémon
const pokemons = ref(["Pikachu", "Bulbizarre", "Salamèche", "Carapuce", "Rondoudou"]);

// Supprimer un Pokémon de la liste
const removePokemon = (index) => {
  pokemons.value.splice(index, 1);
};
</script>
