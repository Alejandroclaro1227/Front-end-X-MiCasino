<template>
  <div>
    <img src="./assets/micasino.png" class="logo" alt="MiCasino logo" />
    <FormComponent :fieldDefinitions="fieldDefinitions" />
  </div>
</template>

<script setup lang="ts">
import FormComponent from './components/FormComponent.vue';

let fieldDefinitions = [
  {
    id: 'name',
    label: 'Nombre',
    type: 'Text',
    required: true,
  },
  {
    id: 'options',
    label: 'Options',
    type: 'SelectUnselect',
    options: [
      { id: '1', label: 'Option 1', status: 'Available' },
      { id: '2', label: 'Option 2', status: 'Disabled' },
      { id: '3', label: 'Option 3', status: 'Disabled' },
    ],
    required: true,
  }
];
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  margin-bottom: 2em;
}
</style>