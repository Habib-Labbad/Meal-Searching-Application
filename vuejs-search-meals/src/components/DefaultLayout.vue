<template>
  <div class="bg-gray-full">
    <navbar />
    <main>
      <router-view />
    </main>
  </div>
</template>
<script setup>
import navbar from "../components/Navbar.vue";
</script>