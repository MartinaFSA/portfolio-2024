<template>
  <header>
        <div class="hamburguerIcon">
            <div class="topBar"></div>
            <div class="bottomBar"></div>
        </div>
        <nav id="navbar">
          <ul id="ctnNavLinks">
              <li><a href="#inicio">Inicio</a></li>
              <li v-if="isPortlioPage"><a href="#proyectos">Proyectos</a></li>
              <li v-else><RouterLink to="/#proyectos">Proyectos</RouterLink></li>
              <li><a href="#contacto">Contacto</a></li>
          </ul>
        </nav>
    </header>
</template>

<script setup lang="ts">
    import { onBeforeMount, onMounted, ref } from 'vue';
    import { RouterLink } from 'vue-router';

    window.onscroll = function() {scrollFunction()};

    const screenHeight = window.screen.height * window.devicePixelRatio;
    const isPortlioPage = ref(false);

    onBeforeMount(() => {
        getPathDir();
    })
    onMounted(() => {
        setTimeout(() => {
            getPathDir();
        }, 1000);
    })

    //FUNCTIONS
    function scrollFunction() {
        const navarEl = document.getElementById("navbar")
        if (document.body.scrollTop > screenHeight || document.documentElement.scrollTop > screenHeight) {
            if(navarEl) {
                navarEl.style.opacity = "1";
                navarEl.style.top = "0";
            }
        } else {
            if(navarEl) {
                navarEl.style.top = "-50px";
                navarEl.style.opacity = "0";
            }
        }
    }

    function getPathDir () {
        const windowLocation =  window.location.href.slice(7); //delete http:// from variable
        const firstSlash = windowLocation.indexOf('/') + 1;
        const secondSlash = windowLocation.indexOf('/', firstSlash)  + 1;
        const thirdSlash = windowLocation.indexOf('/', secondSlash) + 1;
        
        const startsWithPortfolioRoute = windowLocation.slice(firstSlash, secondSlash) == "/" ? true : false;
        const pointsToOtherRoute = (windowLocation.slice(secondSlash, thirdSlash) == "#inicio" && windowLocation.slice(secondSlash, thirdSlash) == "#contacto") && (windowLocation.slice(secondSlash, thirdSlash) == "#proyectos") ? true : false;
        isPortlioPage.value = (startsWithPortfolioRoute && pointsToOtherRoute);
    }
</script>