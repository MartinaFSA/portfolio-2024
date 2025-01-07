<template>
  <main id="inicio">
      <section class="positionRelative">
          <div class="positionRelative">
              <h1 class="slideInRight">Martina Fernandez</h1>
              <h1 id="name_indentation" class="slideInLeft">Suarez Anzorena</h1>
              <img class="star focus-in" id="landing_star" src="/src/assets/img/star.svg" alt="">
          </div>
          <h2 class="slideInRight">Web Developer</h2>
          <!-- <div id="ctn_myImg" class="focus-in">
              <div id="bkg_gradient"></div>
              <img id="myImg" src="/src/assets/img/yo.jpg" alt="Portrait picture of Martina">
          </div> -->
          <div class="positionRelative focus-in">
              <!-- <div class="arc" id="landing_firstArc"></div>
              <div class="arc" id="landing_sndArc"></div> -->
              <div class="line" id="landing_line"></div>
              <div class="halfCircle" id="landing_halfCircle"></div>
          </div>
      </section>

      <section id="proyectos">
          <h3>Proyectos</h3>
          <section id="content-archive" role="main">
              <div class="thumbnail" v-for="(project, index) in projects" :key="index">
                  <div class="positionRelative">
                      <RouterLink :to="'project/' + project.objectName" rel="bookmark">
                          <div></div>
                          <img :src="'/src/assets/img/projects/' + project.img" alt="" loading="lazy">
                      </RouterLink>
                  </div>
                  <div class="hover">
                      <RouterLink :to="'project/' + project.objectName" :title="project.title" rel="bookmark">
                          <p class="project_title">{{project.title}}</p>
                          <p class="tags">{{ project.tag }}</p>
                      </RouterLink>
                  </div>
              </div>
          </section>
      </section>
      <Contact></Contact>
  </main>
</template>
<script setup lang="ts">
import { ref, onBeforeMount } from 'vue';
import { RouterLink } from 'vue-router';
import Contact from '../components/Contact.vue';
import projectsJson from '../assets/data/projectsData.json';
import experiencesJson from '../assets/data/experiencesData.json';
import type { IExperience } from '../assets/data/models';

const projects = ref<any[]>(projectsJson);
const experiences = ref<IExperience[]>([]);
onBeforeMount(() => {
    experiences.value = experiencesJson;
    console.log(projectsJson)
    console.log(experiencesJson)
});

const calculateTotalWorked = (experience: IExperience) => {
  const fromTime = new Date(experience.fromTime);
  const toTime = new Date(experience.toTime);

  const yearsWorked = toTime.getFullYear() - fromTime.getFullYear();
  const monthsWorked = toTime.getMonth() - fromTime.getMonth();
  let totalTime = ''; 

  switch (yearsWorked) {
    case 0:
      break;
    case 1:
      totalTime += '1 year';
      break;
    default:
      totalTime += yearsWorked + ' years';
      break;
  }

  switch (monthsWorked) {
    case 0:
      break;
    case 1:
      totalTime += ', 1 month';
      break;
    default:
      totalTime += ', ' + monthsWorked + ' months';
      break;
  }
  
  return totalTime;
};

</script>
<style>
  @import '../assets/styles/portfolio.css';
</style>