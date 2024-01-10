<template>
  <div class="p-8 pb-0">
    <input
      type="text"
      class="rounded border-2 border-gray-200 w-full outline-none border-transparent focus:border-transparent transition-all"
      placeholder="Search for meals"
      v-model="keyword"
      @change="searchMeals"
    />
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
</template>
<script setup>
import MealItem from "../components/MealItem.vue";
import { computed, onMounted, ref } from "vue";
import store from "../store";
import { useRoute } from "vue-router";

const route = useRoute();

let keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

const searchMeals = () => {
  store.dispatch("searchMeals", keyword.value);
};

onMounted(() => {
  keyword.value = route.params.name;

  if (keyword.value) {
    searchMeals();
  }
});
</script>
