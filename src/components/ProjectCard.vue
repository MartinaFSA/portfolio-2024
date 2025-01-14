<template>
    <article class="projectCard">
        <div class="projectName whiteText">
            <p class="h3">{{project.title}}</p>
            <a :href="project.link" aria-labelledby="Visit site" target="_blank"><img src="/arrow.svg" alt=""></a>
        </div>
        <a class="projectImg" @click="openModal(project)">
            <img :src="project.img" alt="">
            <div class="readMore"><p class="h4">Read more</p></div>
        </a>
        <div class="projectInfo whiteText">
            <p class="generalText">{{project.owner}}</p>
            <p class="generalText">{{project.design}}</p>
        </div>
    </article>
</template>

<script setup lang="ts">
    import { defineEmits } from 'vue';
    const emits = defineEmits(['projectSelected']); 

    defineProps({
        project: {
            type: Object,
            required: true,
        },
    });
    
    function openModal(projectObj: any) {
        emits('projectSelected', projectObj);
    }
</script>