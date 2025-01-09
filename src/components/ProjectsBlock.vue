<script setup lang="ts">
import ProjectCard from '@/components/ProjectCard.vue';
import projectsJson from '../assets/data/projectsData.json';
import { onBeforeMount, ref } from 'vue';

const projects = ref<any[]>(projectsJson);
onBeforeMount(() => {
    projects.value = projectsJson;
    console.log(projectsJson)
});

</script>


<template>
    <section id="ctn_projects">
      <div class="cards">
        <ProjectCard />
        <ProjectCard />
        <ProjectCard />
        <ProjectCard />
        <ProjectCard />
        <ProjectCard />
        <ProjectCard />
        <ProjectCard />
      </div>
      <div class="gsap-scroll-trigger titleBox">
        <h2 class="title">Works</h2>
      </div>
    </section>
</template>