<template>
  <main id="home">
    <section id="ctn_name">
      <div>
        <h1>
          Martina Fernandez
          <br>Suarez Anzorena
        </h1>
        <div class="asterisk">
          <img src="/asterisk.svg" alt="">
        </div>
      </div>
      <div class="leftMargin whiteText">
          <div class="single-line">
            <div class="single-line-inner">
              <p class="generalText">Trabajo realizado Para el estudio Aguaviva</p>
            </div>
          </div>
          <div class="single-line">
            <div class="single-line-inner">
              <p class="generalText">Diseñado por Aguaviva Trabajo realizado</p>
            </div>
          </div>
          <div class="single-line">
            <div class="single-line-inner">
              <p class="generalText">Diseñado por Aguaviva</p>
            </div>
          </div>
      </div>
      <div id="webDev">
        <h2>Web Developer</h2>
      </div>
    </section>
    <section id="works">
      <ProjectsBlock/>
    </section>
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

<style lang="scss">
.single-line {
  display: block;
  position: relative;
  overflow: hidden;
  margin: -0.4em -0.1em;
  
  .single-line-inner {
    translate: none;
    rotate: none;
    scale: none;
    position: relative;
    display: inline-block;
    padding: 0.2em 0.1em;
    animation: slideText 0.5s cubic-bezier(.09,.64,.69,.85) forwards;
    opacity: 0;
  }
  &:nth-of-type(2) {
    .single-line-inner {
      animation-delay: 0.2s;
    }
  }
  &:nth-of-type(3) {
    .single-line-inner {
      animation-delay: 0.4s;
    }
  }
}
@keyframes slideText {
  0% {
    transform: translate(0%, 100%) translate3d(0px, 0px, 0px) rotate(0.001deg);
    opacity: 0;
  }
  100% {
    transform: translate(0%, 0%) translate3d(0px, 0px, 0px) rotate(0.001deg);
    opacity: 1;
  }
}
</style>