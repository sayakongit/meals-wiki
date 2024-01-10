<template>
  <div class="bg-white shadow-md rounded-xl">
    <img
      :src="meal.strMealThumb"
      :alt="meal.strMeal"
      class="rounded-t-xl h-48 w-full object-cover"
    />

    <div class="p-3">
      <h3 class="font-semibold">{{ meal.strMeal }}</h3>
      <div class="mt-4 flex gap-4 items-center">
        <a
          :href="meal.strYoutube"
          target="_blank"
          class="px-3 py-2 text-xs rounded border-2 border-red-500 bg-red-500 text-white hover:bg-red-600 hover:border-red-600 transition-all"
          >YouTube</a
        >
        <router-link
          :to="{ name: 'mealDetails', params: { id: meal.idMeal } }"
          class="px-3 py-2 text-xs rounded border-2 hover:bg-gray-100 transition-all"
        >
          View
        </router-link>
      </div>
    </div>
  </div>
</template>
<script setup>
const { meal } = defineProps({
  meal: Object,
});
</script>
