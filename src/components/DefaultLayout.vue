<template>
  <div class="">
    <Navbar />
    <main>
      <router-view />
    </main>
  </div>
</template>
<script setup>
import Navbar from "./Navbar.vue";
</script>
