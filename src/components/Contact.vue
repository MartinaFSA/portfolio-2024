<template>
    <footer class="positionRelative" id="contacto">
        <h1>Reach Out</h1>
        <div class="footer_social-list">
            <div>
                <a href="https://github.com/MartinaFSA" target="_blank" class="social-link" aria-labelledby="Go to GitHub">
                    <div class="social-icon">
                        <GithubIcon/>
                    </div>
                </a>
                <a href="https://www.linkedin.com/in/martina-fernandez-suarez/" target="_blank" class="social-link" aria-labelledby="Go to LinkedIn">
                    <div class="social-icon">
                        <LinkedInIcon/>
                    </div>
                </a>
            </div>
            <a href="mailto:martinafsa8@gmail.com" class="generalText whiteText" target="_blank">martinafsa8@gmail.com</a>
        </div>
    </footer>
</template>
<script setup lang="ts">
    import LinkedInIcon from './ui/LinkedInIcon.vue'
    import GithubIcon from './ui/GithubIcon.vue'
</script>