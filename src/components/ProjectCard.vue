<template>
    <article class="projectCard">
        <div class="projectName whiteText">
            <p class="h3">{{project.title}}</p>
            <a :href="project.link" aria-labelledby="Visit site" target="_blank"><img src="/arrow.svg" alt=""></a>
        </div>
        <a class="projectImg" @click="openModal(slug(project.title))">
            <img :src="project.img" alt="">
            <div class="readMore"><p class="h4">Read more</p></div>
        </a>
        <div class="projectInfo whiteText">
            <p class="generalText">{{project.owner}}</p>
            <p class="generalText">{{project.design}}</p>
        </div>
    </article>
    <section class="modal" :id="slug(project.title)">
        <h2 @click="closeModal">X</h2>
        <div>
            <div class="modal-image">
                <img :src="project.img" alt="">
            </div>
            <div class="modal-text">
                <p class="h3">{{project.title}}</p>
                <p class="generalText">{{project.owner}}</p>
                <p class="generalText">{{project.description}}</p>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
    defineProps({
        project: {
            type: Object,
            required: true,
        },
    });
    function slug(string: string) {
        let str = string.replace(/[A-Z]/g, '');
        str = str.replace(/\s+/g, '-');

        const accents: { [key: string]: string } = {
            'á': 'a', 'é': 'e', 'í': 'i', 'ó': 'o', 'ú': 'u',
            'Á': 'a', 'É': 'e', 'Í': 'i', 'Ó': 'o', 'Ú': 'u',
            'ñ': 'n', 'Ñ': 'n'
        };

        str = str.split('').map((char: string) => accents[char] || char).join('');

        return str;
    }
    function openModal(title: string) {
        const modal = document.getElementById(title);
        if(modal)
            modal.classList.add('show');
        return;
    }
    function closeModal() {
        const modal = document.querySelector('.modal.show');
        if(modal)
            modal.classList.remove('show');
        return;
    }
</script>

<style lang="scss">
    .modal {
        display: none;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 20;
        width: 100vw;
        height: 100vh;
        background-color: rgba(0, 0, 0, 0.582);
        justify-content: center;
        align-items: center;
        padding: 50px;
        &.show {
            display: flex;
        }
        > div {
            background-color: var(--white);
            width: 80%;
            height: 80%;
            max-width: 1140px;
            overflow: scroll;
            display: flex;
            gap: 10%;
            padding: 5rem;
            .modal-image {
                width: 50%;
                height: fit-content;
                overflow: visible;
                img {
                    width: 100%;
                    object-fit: contain;
                }
            }
            .modal-text {
                width: 50%;
                height: fit-content;
                overflow: visible;
                color: var(--black);
            }
        }
    }
</style>