<script setup lang="ts">
import ProjectCard from '@/components/ProjectCard.vue';
import projectsJson from '../assets/data/projectsData.json';
import { onBeforeMount, onMounted, onUnmounted, ref } from 'vue';
// import gsap from 'gsap';
// import { ScrollTrigger } from 'gsap/ScrollTrigger';

const projects = ref<any[]>(projectsJson);
onBeforeMount(() => {
  projects.value = projectsJson;
});

// onMounted(() => {
//   gsap.registerPlugin(ScrollTrigger);
//     gsap.fromTo('.gsap-scroll-trigger',
//       {
//         position: 'absolute',
//         display: 'none',
//       },
//       {
//         position: 'fixed',
//         display: 'flex',
//         top: '30%',
//         duration: 2,
//         // ease: 'power1.out',
//         scrollTrigger: {
//           trigger: '.cards',
//           start: 'top 50%',
//           scrub: true,
//           markers: false,
//           id: 'scroll-trigger',
//         },
//     });
// })

// onUnmounted(() => {
//   ScrollTrigger.getAll().forEach((trigger) => trigger.kill());
// });

</script>


<template>
    <section id="ctn_projects">
      <h2 class="title orangeText">Works</h2>
      <div class="cards">
        <div v-for="(project, i) in projects" :key="i">
          <ProjectCard :project="project"/>
        </div>
      </div>
      <!-- <div class="gsap-scroll-trigger titleBox">
        <h2 class="title">Works</h2>
      </div> -->
    </section>
</template>