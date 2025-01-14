<script setup lang="ts">
  import { RouterView } from 'vue-router';
  // import Navbar from './components/Navbar.vue';
  import Contact from './components/Contact.vue';
</script>

<template>
  <section>
    <!-- <Navbar /> -->
    <RouterView />
    <Contact></Contact>
  </section>
</template>