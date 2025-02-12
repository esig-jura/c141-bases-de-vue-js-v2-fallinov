<script setup>
// Déclaration des props
import { defineProps } from 'vue'
// Déclaration des props
const props = defineProps({
  texte: String,
  color: String
})
// Déclaration des événement émis
const emit = defineEmits(['salut'])

</script>

<template>
  <p :style="'color: ' + color">
    <slot></slot>
    <v-btn @click="emit('salut', 'Jeanne')">Salut !</v-btn>
    <slot name="footer"></slot>
  </p>
</template>

<style scoped lang="sass">
  p
    border: 3px solid red
    padding: 10px
    box-shadow: #C6FF00 0px 0px 10px
</style>
