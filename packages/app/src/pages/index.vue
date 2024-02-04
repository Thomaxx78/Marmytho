<script lang="ts" setup>

const { find } = useStrapi()

// useAsyncData('recipes', () =>find('recipes'))
const { data:recipes, pending, error, refresh } = useAsyncData(
  'recipes',
  () => find('recipes',{
    populate:'*',
  })
)
</script>

<template>
  <div class="container">
    <div class="">
      <div v-if="recipes">
        <ul class="grid grid-cols-4 list-none gap-8">
          <li class="max-w-full" v-for="recipe in recipes.data" :key="recipe.id">
            <NuxtImg class="w-full aspect-ratio-square" v-if="recipe.image && recipe.image.url" :src="recipe.image.url" :alt="recipe.title" />
            <h3>{{ recipe.title }}</h3>
            <div class="line-clamp-3">
              <p>{{ recipe.description }}</p>
            </div>
            <NuxtLink class="mt-4" :to="`/recettes/${recipe.slug}`">Voir la recette</NuxtLink>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>