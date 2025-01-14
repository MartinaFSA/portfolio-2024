<template>
    <header>
        <section class="header">
            <a class="hamburguerIcon cross" @click="toggleMenu">
                <div class="topBar"></div>
                <div class="bottomBar"></div>
            </a>
            <nav id="navbar">
                <ul id="ctnNavLinks">
                    <li><a href="/#works" class="h3 whiteText">Works</a></li>
                    <!-- <li><a href="/about" class="h3 whiteText">About me</a></li> -->
                    <li><a href="#contact" class="h3 whiteText">Contact</a></li>
                </ul>
            </nav>
        </section>
    </header>
</template>

<script setup lang="ts">
    window.onscroll = function() {scrollFunction()};

    const screenHeight = window.screen.height * window.devicePixelRatio;

    //FUNCTIONS
    function scrollFunction() {
        const headerEl = document.querySelector(".header");
        const navarEl = document.querySelector("nav");
        const hamburguerIcon = document.querySelector(".hamburguerIcon");

        if (document.body.scrollTop > screenHeight || document.documentElement.scrollTop > screenHeight) {
            if(headerEl) {
                headerEl.classList.add("show");
            }
        } else {
            if(headerEl && navarEl && hamburguerIcon) {
                headerEl.classList.remove("show");
                navarEl.classList.remove("show");
                hamburguerIcon.classList.remove("opened");
            }
        }
    }
    function toggleMenu() {
        const navarEl = document.querySelector("nav");
        const hamburguerIcon = document.querySelector(".hamburguerIcon");
        if(navarEl && hamburguerIcon) {
            navarEl.classList.toggle("show");
            hamburguerIcon.classList.toggle("opened");
        }
    }
</script>