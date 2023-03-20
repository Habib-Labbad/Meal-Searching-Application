<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold text-orange-500 mb-4">Ingredients</h1>
    <input
      type="text"
      v-model="keyword"
      class="rounded border-2 border-grey-200 w-full mb-6"
      placeholder="Search for Ingredient"
    />
    <router-link
      :to="{ name: 'byIngredient', params: { ingredient: meal.strIngredient } }"
      v-for="meal of ingredients"
      :key="meal.idIngredient"
      class="block bg-white rounded p-3 mb-3 shadow"
    >
      <h3 class="text-2xl font-bold mb-2 text-red-500">
        {{ meal.strIngredient }}
      </h3>
      <p>{{ meal.strDescription }}</p>
    </router-link>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient.js";

const route = useRoute();
const meals = ref([]);
const keyword = ref("");
const ingredients = computed(() => {
  if (!ingredients) return meals;
  return meals.value.filter((i) => {
    return i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase());
  });
});
onMounted(() => {
  axiosClient.get(`list.php?i=list`).then(({ data }) => {
    meals.value = data.meals.slice(0, 36);
  });
});
</script>