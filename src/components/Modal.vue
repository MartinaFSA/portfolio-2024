<template>
    <section class="modal">
        <div>
            <div @click="closeModal" class="closeModal cross">
                <div class="crossbar topBar"></div>
                <div class="crossbar bottomBar"></div>
            </div>
            <div class="modal-body">
                <div class="modal-text">
                    <div>
                        <p class="h3">{{project.title}}</p>
                        <p class="generalText orangeText">{{project.date}}</p>
                        <p class="generalText">{{project.description}}</p>
                        <p class="generalText">Made with: <span class="orangeText">{{project.development}}</span></p>
                    </div>
                </div>
                <div class="modal-image">
                    <img :src="project.preview" alt="">
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
    import { defineEmits } from 'vue';
    const emits = defineEmits(['closeModal']); 

    defineProps({
        project: {
            type: Object,
            required: true,
        },
    });
    function closeModal() {
        emits('closeModal');
        return;
    }
</script>