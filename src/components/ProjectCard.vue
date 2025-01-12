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
            position: relative;
            .closeModal {
                position: absolute;
                top: -35px;
                right: -35px;
                z-index: 3;
                color: var(--accent-color);
            }
            .modal-body {
                height: 100%;
                overflow-y: auto;
                padding-right: 3px;
                .modal-image {
                    height: fit-content;
                    overflow: visible;
                    img {
                        width: 100%;
                        object-fit: contain;
                    }
                }
                .modal-text {
                    overflow: visible;
                    color: var(--black);
                    margin-bottom: 50px;
                    > div {
                        p {
                            width: fit-content;
                        }
                    }
                    .h3 {
                        margin-bottom: 20px;
                    }
                }
            }
        }
    }
    @media screen and (max-width: 865px) {
        .modal {
            > div {
                width: 90%;
                height: 90%;
            }
        }
    }
    
    @media screen and (max-width: 985px) {
        .modal > div {
            padding: 20px 30px;
        }
    }
    @media screen and (min-width: 985px) {
        .modal {
            > div {
                padding: 3rem 20px 3rem 3rem;
                .modal-body {
                    padding-right: 3rem;
                    display: flex;
                    flex-direction: row-reverse;
                    gap: 50px;
                    .modal-image {
                        width: 65%;
                    } .modal-text {
                        width: 35%;
                        > div {
                            position: fixed;
                            width: 23%;
                        }
                    }
                }
            }
        }
    }
</style>