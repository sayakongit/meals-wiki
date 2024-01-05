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
    <div
      v-for="meal of meals"
      :key="meal.idMeal"
      class="bg-white shadow-md rounded-xl"
    >
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
            to="/"
            class="px-3 py-2 text-xs rounded border-2 hover:bg-gray-100 transition-all"
          >
            View
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { computed, onMounted, ref } from "vue";
import axiosClient from "../axiosClient";
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
