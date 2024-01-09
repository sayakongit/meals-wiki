<template>
  <div
    class="max-w-[1200px] mt-10 mx-auto flex flex-col md:flex-row gap-5 md:gap-10 px-4 md:px-8"
  >
    <div class="md:w-[50%]">
      <img :src="meal.strMealThumb" :alt="meal.strMeal" class="" />
    </div>

    <div class="md:w-[50%]">
      <h1 class="text-4xl font-semibold mb-5">{{ meal.strMeal }}</h1>
      <div class="">
        <div>
          <strong class="font-medium">Category:</strong> {{ meal.strCategory }}
        </div>
        <div><strong class="font-medium">Area:</strong> {{ meal.strArea }}</div>
        <div v-if="meal.strTags">
          <strong class="font-medium">Tags:</strong> {{ meal.strTags }}
        </div>
      </div>

      <div class="my-4 w-full">
        <table
          class="w-full text-left rtl:text-right text-gray-500 dark:text-gray-400"
        >
          <thead
            class="text-gray-700 bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
          >
            <tr>
              <th scope="col" class="px-6 py-3 font-semibold">Ingredients</th>
              <th scope="col" class="px-6 py-3 font-semibold">Measures</th>
            </tr>
          </thead>
          <tbody>
            <template v-for="(el, ind) of new Array(20)">
              <tr
                class="bg-white border-b dark:bg-gray-800 dark:border-gray-700"
                v-if="meal[`strIngredient${ind + 1}`]"
              >
                <td
                  scope="row"
                  class="px-6 py-3 text-gray-900 whitespace-nowrap dark:text-white"
                >
                  {{ meal[`strIngredient${ind + 1}`] }}
                </td>
                <td class="px-6 py-3">
                  {{ meal[`strMeasure${ind + 1}`] }}
                </td>
              </tr>
            </template>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";

const route = useRoute();
const meal = ref({});

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || {};
    console.log(data);
  });
});
</script>
