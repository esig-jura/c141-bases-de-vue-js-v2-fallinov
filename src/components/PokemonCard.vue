<template>
  <v-list-item>
    <v-list-item-title>
      {{ pokeNom }}
    </v-list-item-title>

    <template v-slot:append>
      <v-btn
        icon="mdi-delete"
        variant="text"
        @click="deletePokemon"
      ></v-btn>
    </template>
  </v-list-item>
</template>

<script setup>
// Définition des propriétés du composant
const props = defineProps({
  pokeNom: {
    type: String,
    required: true,
  },
})

// Définition des événements du composant
const emit = defineEmits(['delete'])

// Fonction qui émet l'événement delete
function deletePokemon () {
  // Si l'utilisateur confirme la suppression
  if(confirm(`Voulez-vous vraiment supprimer ${ props.pokeNom } ?`)) {
    // Émission de l'événement delete
    emit('delete')
  }
}

</script>

<style scoped lang="sass">

</style>
