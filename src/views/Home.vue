<template>
  <div class="flex flex-col p-8 justify-center">
    <div class="flex justify-center gap-2 mt-2">
      <router-link
        :to="{ name: 'byLetter', params: { letter } }"
        v-for="letter in letters"
        :key="letter"
      >
        {{ letter }}
      </router-link>
    </div>
  </div>
</template>
<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import axiosClient from "../axiosClient";

const meals = computed(() => store.state.meals);

const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const mealsArr = ref();

onMounted(async () => {
  const res = await axiosClient.get("/list.php?i=list");

  console.log(res.data);
});
</script>
<style></style>
