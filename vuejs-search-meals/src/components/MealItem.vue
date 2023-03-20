<template>
  <div :key="meal.idMeal" class="bg-white shadow">
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
      <img
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
        class="rounded-t-xl w-full h-48 object-cover"
      />
    </router-link>
    <div class="p-3">
      <h3 class="font-bold">{{ meal.strMeal }}</h3>
      <div class="mb-4">
        <p v-if="meal.strInstructions">
          {{ meal.strInstructions.slice(0, 200) }}
        </p>
      </div>
      <div class="flex items-center justify-between">
        <YouTubeButton :href="meal.strYoutube"> YouTube</YouTubeButton>
      </div>
    </div>
  </div>
</template>

<script setup>
import YouTubeButton from "../components/YouTubeButton.vue";

const { meal } = defineProps({
  meal: {
    required: true,
    type: Object,
  },
});
</script>