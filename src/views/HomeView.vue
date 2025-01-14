<template>
  <main id="home">
    <section class="ctn_name">
      <section class="fixed">
        <div class="name">
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
                <p class="generalText">Passionate about creating modern websites.</p>
              </div>
            </div>
            <div class="single-line">
              <div class="single-line-inner">
                <p class="generalText">Always looking forward to finding new</p>
              </div>
            </div>
            <div class="single-line">
              <div class="single-line-inner">
                <p class="generalText">challenging projects.</p>
              </div>
            </div>
        </div>
        <div id="webDev" class="first-scroll single-line">
          <div class="single-line-inner">
            <p>Web Developer</p>
          </div>
        </div>
      </section>
    </section>
    <section id="works" class="second-scroll">
      <div id="ctn_projects">
        <h2 class="title orangeText">Works</h2>
        <div class="cards">
          <div v-for="(project, i) in projects" :key="i">
            <ProjectCard :project="project" @projectSelected="handleModal"/>
          </div>
        </div>
      </div>
    </section>
    <Modal :project="projectSelected" v-if="viewModal" @closeModal="closeModal"/>
  </main>
</template>
<script setup lang="ts">
  import { onBeforeMount, onMounted, onUnmounted, ref } from 'vue';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import Modal from '@/components/Modal.vue';
  import ProjectCard from '@/components/ProjectCard.vue';
  import projectsJson from '../assets/data/projectsData.json';

  //PROJECTS
  const projects = ref<any[]>(projectsJson);
  const viewModal = ref(false);
  const projectSelected = ref()
  
  onBeforeMount(() => {
    projects.value = projectsJson;
  });

  function handleModal (project: any) {
    projectSelected.value = project;
    viewModal.value = true;
    return;
  }

  function closeModal() {
    viewModal.value = false;
    return;
  }

  //SCROLL ANIMATIONS
  onMounted(() => {
    gsap.registerPlugin(ScrollTrigger);
    var tl = gsap.timeline();
    tl.fromTo('.first-scroll',
      {
        xPercent: 0,
      },
      {
        xPercent: 200,
        duration: 2.5,
        ease: "power1.inOut",
        scrollTrigger: {
          trigger: '#home',
          start: '30% 30%',
          end: 'bottom 80%',
          scrub: true,
          markers: false,
          id: 'trigger-1',
        }
    });
    tl.fromTo('#works',
      {
        yPercent: 100,
      },
      {
        duration: 3,
        yPercent: 0,
        ease: 'power2.inOut',
        scrollTrigger: {
          trigger: '#home',
          start: 'top 0%',
          end: 'bottom 20%',
          scrub: true,
          markers: false,
          id: 'trigger-2',
        },
      }, '+=9');
  })
  onUnmounted(() => {
    ScrollTrigger.getAll().forEach((trigger) => trigger.kill());
  });

</script>