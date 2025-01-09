<script setup>
  import { RouterView } from 'vue-router';
  import Navbar from '@/components/Navbar.vue';
</script>

<template>
  <section>
    <Navbar></Navbar>
    <RouterView />
  </section>
</template>