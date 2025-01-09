<template>
  <main id="home">
    <section id="ctn_name">
      <div>
        <h1 class="blur-and-threshold">Martina Fernandez <br>Suarez Anzorena</h1>
        <p class="asterisk">*</p>
      </div>
      <div class="leftMargin">
        <p class="generalText">Trabajo realizado Para el estudio Aguaviva
          Diseñado por Aguaviva Trabajo realizado Para el estudio Aguaviva
          Diseñado por Aguaviva</p>
      </div>
      <div id="webDev">
        <h2 class="blur-and-threshold">Web Developer</h2>
      </div>
    </section>
    <ProjectsBlock />
    <Contact></Contact>
  </main>
</template>
<script setup lang="ts">
import { ref, onBeforeMount } from 'vue';
import Contact from '../components/Contact.vue';
import experiencesJson from '../assets/data/experiencesData.json';
import type { IExperience } from '../assets/data/models';
import ProjectsBlock from '@/components/ProjectsBlock.vue';

const experiences = ref<IExperience[]>([]);
onBeforeMount(() => {
  experiences.value = experiencesJson;
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
<style lang="scss" scoped>
.blur-and-threshold { 
  filter: blur(var(--blur)) url(#svgThreshold);
}

</style>