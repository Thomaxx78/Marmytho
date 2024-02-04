<script setup lang="ts">
const { findOne } = useStrapi()
const route = useRoute()

const { data: recipe, pending } = useAsyncData(
  'recipe',
  () => findOne(`recipes/${route.params.slug}`)
);
</script>

<template>
    <div class="container">
      <template v-if="pending">
        <p>Chargement...</p>
      </template>
      <template v-if="recipe">
        <h1>{{ recipe.data.title }}</h1>
        <!-- Affichez d'autres détails de la recette si nécessaire -->
      </template>
      <template v-else>
        <p>Recette non trouvée</p>
      </template>
    </div>
  </template>
